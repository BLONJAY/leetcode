https://leetcode.com/problems/relative-ranks/

https://leetcode.com/problems/relative-ranks/submissions/


# 506. Relative Ranks

Given scores of N athletes, find their relative ranks and the people with the top three highest scores, who will be awarded medals: "Gold Medal", "Silver Medal" and "Bronze Medal".
Example 1: 
Input: [5, 4, 3, 2, 1]
Output: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
Explanation: The first three athletes got the top three highest scores, so they got "Gold Medal", "Silver Medal" and "Bronze Medal". 
For the left two athletes, you just need to output their relative ranks according to their scores.


---

    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
            nums.sort
            
            for (code, n) in nums {
                print("\(code): \(n)")
            }
            return ["1"]
        }
    }


Compile Error

Line 4: Char 9: error: cannot use mutating member on immutable value: 'nums' is a 'let' constant in solution.swift
        nums.sort
        ^~~~
Line 6: Char 26: error: expression type '[Int]' is ambiguous without more context in solution.swift
        for (code, n) in nums {
                         ^~~~


---


第二個 錯誤是 因為  這個方法是 Dictonary的

---

    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
            //nums.sort

        for (index, value) in nums.enumerate()  {
            print("Item \(index + 1): \(value)")
        }
            return ["1"]
        }
    }



Compile Error

Line 6: Char 27: error: value of type '[Int]' has no member 'enumerate'; did you mean 'enumerated'? in solution.swift
    for (index, value) in nums.enumerate() {
                          ^~~~ ~~~~~~~~~

---
    for (index, value) in nums.enumerated {
        print("Item \(index + 1): \(value)")
    }


Compile Error

Line 6: Char 32: error: type '() -> EnumeratedSequence<[Int]>' does not conform to protocol 'Sequence' in solution.swift
    for (index, value) in nums.enumerated {
                               ^
——————————


    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
        nums.sort

        for item in nums {
            print(item)
        }
            return ["1"]
        }
    }


Compile Error

Line 4: Char 5: error: cannot use mutating member on immutable value: 'nums' is a 'let' constant in solution.swift
    nums.sort
    ^~~~



——————————
    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
        var vNums = nums
        
        for item in vNums {
            print(item)
        }
            

            return ["1"]
        }
    }

—————————




    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
        var vNums = nums
        
        for item in vNums {
            print(item)
        }
            
        vNums.sort
            
        for item in vNums {
            print(item)
        }
            return ["1"]
        }
    }


Compile Error



Line 10: Char 11: error: partial application of 'mutating' method is not allowed in solution.swift
    vNums.sort
          ^
Line 10: Char 11: error: expression resolves to an unused function in solution.swift
    vNums.sort
    ~~~~~~^~~~


---

    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
        var vNums = nums
        
        for item in vNums {
            print(item)
        }
            
            
        vNums.sort(by: >)    
            
        var ansStrings = vNums.map { (n) -> String in
            return String(n)
        }
            
        
            return ansStrings
        }
    }

[4,5,2,1,3]

4
5
2
1
3

["5","4","3","2","1"]

["Silver Medal","Gold Medal","4","5","Bronze Medal"]

——

class Solution {
    func findRelativeRanks(_ nums: [Int]) -> [String] {
        
    var vNums = nums
   
    let goldValue = vNums.max()
    print("\(goldValue)")
    
        
    var ansStrings = vNums.map { (n) -> String in
        return String(n)
    }
        
    
        return ansStrings
    }
}



[4,5,2,1,3]

Optional(5)

["4","5","2","1","3"]

["Silver Medal","Gold Medal","4","5","Bronze Medal"]



---

How to remove an element of a given value from an array in Swift


    let goldValue = vNums.max()
    print("\(goldValue)")
    let farray = arr.filter {$0 != "b"} 
        
本來想  
取出 max存到    金String    刪掉max
取出 max存到    銀String    刪掉max
取出 max存到    銅String    刪掉max


---

先 sort  vNums.sort(by: >)     

再取前三個 值

然後在 map 中換掉




    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
        var vNums = nums
        vNums.sort(by:>)
            
        //let gold = vNums[0]
        // print("vNums[0] = \(vNums[0])")
            
        var ansStrings = nums.map { (n) -> String in
            switch n {
                case vNums[0]:
                    return "Gold Medal"
                case vNums[1]:
                    return "Silver Medal"
                case vNums[2]:
                    return "Bronze Medal"
                default:
                    return String(n)
                
            }
            
        }

        
            return ansStrings
        }
    }


[4,5,2,1,3]

["Silver Medal","Gold Medal","2","1","Bronze Medal"]

["Silver Medal","Gold Medal","4","5","Bronze Medal"]


沒有把剩下的分數 換成排名

---

Map 中讀到某個值
拿去sort中查 該value 的index

swift array find index of value

let arr = ["a","b","c","a"]

let indexOfA = arr.firstIndex(of: "a") // 0
let indexOfB = arr.lastIndex(of: "a") // 3

那同分數的要考慮嗎
題目說不用



    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
            var vNums = nums
            vNums.sort(by:>)

            //let gold = vNums[0]
            // print("vNums[0] = \(vNums[0])")

            var ansStrings = nums.map { (n) -> String in
                switch n {
                    case vNums[0]:
                        return "Gold Medal"
                    case vNums[1]:
                        return "Silver Medal"
                    case vNums[2]:
                        return "Bronze Medal"
                    default:
                        let order = vNums.firstIndex(of: n) + 1
                        return String(order)

                }
            }

            return ansStrings
        }
    }


Compile Error



Line 19: Char 35: error: value of optional type 'Array<Element>.Index?' (aka 'Optional<Int>') must be unwrapped to a value of type 'Array<Element>.Index' (aka 'Int') in solution.swift
                let order = vNums.firstIndex(of: n) + 1
                                  ^

因為可能是我要+1
 let order = vNums.firstIndex(of: n)! + 1
這樣就能通過

---
第一版可以


    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            
            var vNums = nums
            vNums.sort(by:>)

            //let gold = vNums[0]
            // print("vNums[0] = \(vNums[0])")

            var ansStrings = nums.map { (n) -> String in
                switch n {
                    case vNums[0]:
                        return "Gold Medal"
                    case vNums[1]:
                        return "Silver Medal"
                    case vNums[2]:
                        return "Bronze Medal"
                    default:
                        let order = vNums.firstIndex(of: n)! + 1
                        return String(order)

                }
            }

            return ansStrings
        }
    }


---
考量其他情況

優化



    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
            var vNums = nums
            vNums.sort(by:>)

            //let gold = vNums[0]
            // print("vNums[0] = \(vNums[0])")

            var ansStrings = nums.map { (n) -> String in
                let order = vNums.firstIndex(of: n)! + 1
                                    
                switch order {
                    case 1:
                        return "Gold Medal"
                    case 2:
                        return "Silver Medal"
                    case 3:
                        return "Bronze Medal"
                    default:
                        return String(order)                                   
                }
            }

            return ansStrings
        }
    }


Success
Details 
Runtime: 2300 ms, faster than 16.67% of Swift online submissions for Relative Ranks.
Memory Usage: 21.4 MB, less than 100.00% of Swift online submissions for Relative Ranks.

---

https://stackoverflow.com/questions/39458282/sort-swift-array-and-keep-track-of-original-index


I would to sort a swift array and keep track of the original indices. 

For example: arrayToSort = [1.2, 5.5, 0.7, 1.3]

indexPosition = [0, 1, 2, 3]

sortedArray = [5.5, 1.3, 1.2, 0.7]

indexPosition = [1, 3, 0, 2]

Is there an easy way of doing this?



Answer 1

Easiest way is with enumerate. Enumerate gives each element in the array an index in the order they appear and you can then treat them separately.

    let sorted = arrayToSort.enumerate().sort({$0.element > $1.element})
    this results in 
    [(.0 1, .1 5.5), (.0 3, .1 1.3), (.0 0, .1 1.2), (.0 2, .1 0.7)]

To get the indices sorted:

    let justIndices = sorted.map{$0.index}   // [1, 3, 0, 2]






    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
    
            let sortResult = nums.enumerated().sorted(by: {$0.element > $1.element})
            let justIndices = sortResult.map{$0.offset}

            var ansStrings = sortResult.map { (n) -> String in
                
                print("HIHI = \(n.offset)")
                return String(n.offset)
                                            
    //             let order = vNums.firstIndex(of: n)! + 1
                                    
    //             switch order {
    //                 case 1:
    //                     return "Gold Medal"
    //                 case 2:
    //                     return "Silver Medal"
    //                 case 3:
    //                     return "Bronze Medal"
    //                 default:
    //                     return String(order)                                   
    //             }
            }

            return ansStrings
        }
    }



Your input
[5,4,3,2,1]

stdout
HIHI = 0
HIHI = 1
HIHI = 2
HIHI = 3
HIHI = 4

Output
["0","1","2","3","4"]

Expected
["Gold Medal","Silver Medal","Bronze Medal","4","5"]


---
試著導入

    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
    
            let sortResult = nums.enumerated().sorted(by: {$0.element > $1.element})
            let justIndices = sortResult.map{$0.offset}

            var ansStrings = nums.map { (n) -> String in
                
    //             print("HIHI = \(n.offset)")
    //             return String(n.offset)
                                            
    //             justIndices[n.offset]
                                    
                let order = justIndices.firstIndex(of: n)! + 1
                                    
                switch order {
                    case 1:
                        return "Gold Medal"
                    case 2:
                        return "Silver Medal"
                    case 3:
                        return "Bronze Medal"
                    default:
                        return String(order)                                   
                }
            }

            return ansStrings
        }
    }


Runtime Error
Fatal error: Unexpectedly found nil while unwrapping an Optional value
Current stack trace:
0    libswiftCore.so                    0x00007f4290bc2050 _swift_stdlib_reportFatalError + 69
1    libswiftCore.so                    0x00007f4290acfdc6 <unavailable> + 3280326
2    libswiftCore.so                    0x00007f4290ad0145 <unavailable> + 3281221
3    libswiftCore.so                    0x00007f42908f7bd0 _fatalErrorMessage(_:_:file:line:flags:) + 19
4                                       0x00005556a7b7b8aa <unavailable> + 18602
5                                       0x00005556a7b7c5fc <unavailable> + 22012
6                                       0x00005556a7b7ba0d <unavailable> + 18957
7                                       0x00005556a7b7c63b <unavailable> + 22075
8    libswiftCore.so                    0x00007f42908e00b0 Collection.map<A>(_:) + 751
9                                       0x00005556a7b7b473 <unavailable> + 17523
10                                      0x00005556a7b7be72 <unavailable> + 20082
11                                      0x00005556a7b7b084 <unavailable> + 16516
12   libc.so.6                          0x00007f428ea03740 __libc_start_main + 240
13                                      0x00005556a7b7ae09 <unavailable> + 15881


---


    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
    
            let sortResult = nums.enumerated().sorted(by: {$0.element > $1.element})
            let justIndices = sortResult.map{$0.offset}

            var ansStrings = nums.map { (n) -> String in
                
    //             print("HIHI = \(n.offset)")
    //             return String(n.offset)
                                            
    //             justIndices[n.offset]
                                    
                let order = justIndices.firstIndex(of: n)
                                    
                switch order {
                    case 1:
                        return "Gold Medal"
                    case 2:
                        return "Silver Medal"
                    case 3:
                        return "Bronze Medal"
                    default:
                        return String(order)                                  
                } 
            }

            return ansStrings
        }
    }



Compile Error
Line 28: Char 28: error: 
cannot invoke initializer for type 'String' with an argument list of type '(Array<Element>.Index?)' in solution.swift
                    return String(order)    


                    default:
                        return String(order)    這行錯了
                        

---

    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
    
            let sortResult = nums.enumerated().sorted(by: {$0.element > $1.element})
            let justIndices = sortResult.map{$0.offset}

            
            
            justIndices.map{ n in
                            
                print("justIndices = \(n)");
            }
            for (i,j) in justIndices.enumerated() {
                print("i = \(i),j = \(j)")
                
            }
            
            var ansStrings = nums.map { (n) -> String in
                
    //             print("HIHI = \(n.offset)")
    //             return String(n.offset)
                                            
    //             justIndices[n.offset]
                            
                
                let order = justIndices[n-1]
                print("n = \(n),order = \(order)")                     
                return "A="                
                // switch order {
                //     case 1:
                //         return "Gold Medal"
                //     case 2:
                //         return "Silver Medal"
                //     case 3:
                //         return "Bronze Medal"
                //     default:
                //         return String(order)                                   
                // }
            }

            return ansStrings
        }
    }

主要測試這兩個功能


            justIndices.map{ n in
                            
                print("justIndices = \(n)");
            }
            for (i,j) in justIndices.enumerated() {
                print("i = \(i),j = \(j)")
                
            }

---


    class Solution {
        func findRelativeRanks(_ nums: [Int]) -> [String] {
            if nums.isEmpty{
                return []
            }
            
            let sortResult = nums.enumerated().sorted(by: {$0.element > $1.element})
            let justIndices = sortResult.map{$0.offset}

            var res = [String](repeating: "", count: nums.count)
            
            for (i,j) in justIndices.enumerated() {
                print("i = \(i),j = \(j)")
                
                switch i {
                    case 0:
                        res[j] = "Gold Medal"
                    case 1:
                        res[j] = "Silver Medal"
                    case 2:
                        res[j] = "Bronze Medal"
                    default:
                        res[j] = "\(i+1)"                                 
                }
            }
            
            
            return res
        }
    }

Runtime: 88 ms, faster than 58.33% of Swift online submissions for Relative Ranks.
Memory Usage: 21.9 MB, less than 100.00% of Swift online submissions for Relative Ranks.
