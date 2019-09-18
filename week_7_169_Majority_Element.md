
---


error
    binary operator == cannot be applied to operands of two anyobject


if(checkValue == value){
改成
if(checkValue === value){

---

    if(count > target){
        return checkValue
    }
            
return checkValue 這行 有 錯誤訊息

'AnyObject' is not convertible to 'Int'; did you mean to use 'as!' to force downcast?

這樣就語法對了

    if(count > target){
        return checkValue as! Int
    }

----
Fatal error: Index out of range
```swift
class Solution {
    func majorityElement(_ nums: [Int]) -> Int {
        let target = nums.count/2
        var mutableNums = nums as [AnyObject]
        
        while(mutableNums.count>0){
            var checkValue = mutableNums[0]
            var count = 1;

            for (index, value) in mutableNums.enumerated(){
                 if(checkValue === value){
                     count+=1
                 }
                 mutableNums.remove(at: index)
            }
            if(count > target){
                return checkValue as! Int
            }
        }
        return 1
    }
}
```

初步分析

            for (index, value) in mutableNums.enumerated(){
                 print("Item \(index + 1): \(value)")
                 if(checkValue === value){
                     count+=1
                 }
                 mutableNums.remove(at: index)
            }

這邊就會有問題

Item 1: 3
Item 2: 2
Item 3: 3

然後就 fatel error

再回頭去看
我剛剛查的  邊for 邊移除

    var a = [1,2,3,4,5,6]
    for (i,num) in a.enumerated().reversed() {
    a.remove(at: i)
    }
    print(a)

所以我少了這個
enumerated().reversed() 

----

沒問題 submit  送出
然後wrong answer

[6,5,5]

打印出來

target = 1
Item 3: 5
Item 2: 5
Item 1: 6
count = 2

原來reverse 會反著來

那我保存第一個 value 就錯了
var checkValue = mutableNums[0]


試著   var checkValue;  先不給初值
代碼如下
一運行就報錯   Line 10: Char 17: error: type annotation missing in pattern 
說你 var checkValue; 這邊有問題

        while(mutableNums.count>0){
            var checkValue;
            var count = 0;

            for (index, value) in mutableNums.enumerated().reversed(){
        
                if(index == 0){
                    checkValue = value
                }

改成
將他初值設為0
下面的比較也要改  後面要加上  as! Int

        while(mutableNums.count>0){
            var checkValue = 0 
            var count = 0

            for (index, value) in mutableNums.enumerated().reversed(){
                
                if(index == 0){
                    checkValue = value as! Int
                }
                
                 if(checkValue == value as! Int){
                     count+=1
                 }

------
[3,2,3]
還是有問題
因為 從後面Item 3: 3
 所以這樣 if(index == 0){ 有問題


            for (index, value) in mutableNums.enumerated().reversed(){
                 print("Item \(index + 1): \(value)")
                
                if(index == 0){
                    checkValue = value as! Int
                }


所以還是直接 在外面讀取值     var checkValue = mutableNums.last

        while(mutableNums.count>0){
            
            var checkValue = mutableNums.last
            var count = 0

            for (index, value) in mutableNums.enumerated().reversed(){

                 if(checkValue === value ){
                     count+=1
                 }
                 mutableNums.remove(at: index)
            }

----

仍然失敗
[3,3,4]

    class Solution {
        func majorityElement(_ nums: [Int]) -> Int {
            
            
            let target = nums.count/2
            //print(target)
            var mutableNums = nums as [AnyObject]
            
            while(mutableNums.count>0){
                
                var checkValue = mutableNums.last
                var count = 0

                for (index, value) in mutableNums.enumerated().reversed(){
                    print("Item \(index + 1): \(value)")
                    print("checkValue = \(checkValue)")
                    print("value = \(value)")
                    if(checkValue === value ){
                        count+=1
                    }
                    mutableNums.remove(at: index)
                }
                print("count = \(count)")
                print("------")
                if(count > target){
                    return checkValue as! Int
                }
            
            }

            
            return 1
        }
    }

打印log

Item 3: 4
checkValue = Optional(4)
value = 4
Item 2: 3
checkValue = Optional(4)
value = 3
Item 1: 3

可能是型別

所以想試著改變型別

    var checkValue = mutableNums.last as ...之類的

    if(checkValue === value )


想說也可以改變 value之類的
就想查一下  swift 打印變數的型別

後來又想到 
是因為if 比較時 型別對不上
checkValue = Optional(4)
所以解開這個 就好

                 if(checkValue!  === value){
                     count+=1
                 }

仍有問題
發現移除時間點怪怪的
                 if(checkValue!  === value){
                     count+=1
                     mutableNums.remove(at: index)
                 }

這樣又可以了

---

又倒在


[-1,100,2,100,100,4,100]


仍然是
if(checkValue!  === value)這邊進不去 count 不會加
改成這樣
if(checkValue! as! Int  == value  as! Int){

最後成功 submit

## Runtime: 648 ms, faster than 5.30% of Swift online submissions for Majority Element.
## Memory Usage: 22.9 MB, less than 33.33% of Swift online submissions for Majority Element.

``` Swift
class Solution {
    func majorityElement(_ nums: [Int]) -> Int {
        
        
        let target = nums.count/2
        print("target = \(target)")
        print("------")
        var mutableNums = nums as [AnyObject]
        
        while(mutableNums.count>0){
            
            var checkValue = mutableNums.last 
            var count = 0

            for (index, value) in mutableNums.enumerated().reversed(){
                 // print("Item \(index + 1): \(value)")
                 // print("checkValue! = \(checkValue!)")
                 // print("value = \(value)")
                 if(checkValue! as! Int  == value  as! Int){
                     count+=1
                     mutableNums.remove(at: index)
                 }
                 // print("目前count = \(count)")
            }
            // print("count = \(count)")
            // print("------")
            if(count > target){
                print("HIHI")
                return checkValue as! Int
            }
           
        }

        
        return 1
    }
}
```


整理一下 自己想的
google了哪些

[語法][1] 
[swift的高階函式][2]


[1]: https://itisjoe.gitbooks.io/swiftgo/content/ch1/collection_types.html
[2]: https://medium.com/%E5%BD%BC%E5%BE%97%E6%BD%98%E7%9A%84-swift-ios-app-%E9%96%8B%E7%99%BC%E6%95%99%E5%AE%A4/array-%E7%9A%84%E9%AB%98%E9%9A%8E%E5%87%BD%E5%BC%8F-filter-map-and-reduce-39fb8ba5a9f7



----
# 別人的
    class Solution {
        func majorityElement(_ nums: [Int]) -> Int {
            return nums.sorted()[nums.count / 2]
        }
    }

## Runtime: 176 ms, faster than 14.95% of Swift online submissions for Majority Element.
## Memory Usage: 21.4 MB, less than 33.33% of Swift online submissions for Majority Element.