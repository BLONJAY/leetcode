
    class Solution {
        func containsDuplicate(_ nums: [Int]) -> Bool {
            nums.sorted()
            
            var temp = 0
            for value in nums {
                print("temp = \(temp), value = \(value)");
                if(temp == value){
                    return true
                }
                temp = value
            }
            return false
        }
    }

打印  感覺沒 sort
temp = 0, value = 1
temp = 1, value = 2
temp = 2, value = 3
temp = 3, value = 1


sorted()回傳排序陣列結果，不影響原陣列內容。
sort()回傳排序陣列結果，並將結果存回原陣列。

試著
    nums.sort(by: <)

cannot use mutating member on immutable value: 'nums' is a 'let' constant in solution.swift
        
試著解決
底下這樣可以
``` swift
    class Solution {
        func containsDuplicate(_ nums: [Int]) -> Bool {
            var mutableNums = nums as [Int]
            mutableNums.sort(by: <)

            var temp = 0
            for value in mutableNums {

                print("temp = \(temp), value = \(value)");

                if(temp == value){
                    return true
                }
                temp = value
            }
            return false
        }
    }
```

submit 
遇  [0]  錯誤
我上面的解法是 sort 後並存回 原本的 array
然後 for  如果有跟上一個值 相同的代表有

可能要排除只以一位的情況

底下 submit 成功
## Runtime: 156 ms, faster than 62.53% of Swift online submissions for Contains Duplicate.
## Memory Usage: 21.9 MB, less than 20.00% of Swift online submissions for Contains Duplicate.
``` swift
class Solution {
    func containsDuplicate(_ nums: [Int]) -> Bool {
        if(nums.count < 2){
            return false
        }
        
        var mutableNums = nums as [Int]
        mutableNums.sort(by: <)

        var temp = 0
        for value in mutableNums {
            // print("temp = \(temp), value = \(value)");
            if(temp == value){
                return true
            }
            temp = value
        }
        return false
    }
}
```