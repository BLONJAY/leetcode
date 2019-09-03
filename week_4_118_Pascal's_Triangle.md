
``` Objective-C
class Solution {
    func generate(_ numRows: Int) -> [[Int]] {
        if numRows == 0 {
            return []
        }
        if numRows == 1 {
            return [[1]]
        }

        var result = Array<Array<Int>>()
        result.append([1])

        var v = [1,1]
        result.append(v)
        if numRows == 2 {
            return result
        }

        for floor in 2...numRows-1 {
            var v = [1]
            for index in 0...result[floor-1].count-2{
                v.append(result[floor-1][index] + result[floor-1][index+1])
            }
            v.append(1)
            result.append(v)
        }
        return result
    }
}
```
