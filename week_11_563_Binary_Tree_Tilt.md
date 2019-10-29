https://leetcode.com/problems/binary-tree-tilt/


 1
2 3
2-3 取絕對值 = 1

                1
        2               3
    9       4        6     2

    先算 2 9 4 --> 5
    再算 3 6 2 --> 4
    再從 1 的斜率  左邊是 15 - 11    斜率是4

    
    開始算整個總協率  5 + 4 + 4



---

        /**
    * Definition for a binary tree node.
    * public class TreeNode {
    *     public var val: Int
    *     public var left: TreeNode?
    *     public var right: TreeNode?
    *     public init(_ val: Int) {
    *         self.val = val
    *         self.left = nil
    *         self.right = nil
    *     }
    * }
    */
    class Solution {
        func findTilt(_ root: TreeNode?) -> Int {
            
            print("root.val = \(root!.val)")
            print("root.left = \(root!.left)")       
            print("root.right = \(root!.right)")
            return 1
        }
        
    }

    Wrong Answer    Runtime: 8 ms

    Your input
     [1,2,3,4,5,6,6]
    stdout
       root.val = 1
         root.left = Optional(TreeNode.TreeNode)
       root.right = Optional(TreeNode.TreeNode)
    Output
               1
    Expected
               5



---
    class Solution {
        func findTilt(_ root: TreeNode?) -> Int {
            
            print("root.val = \(root!.val)")
            print("root.left = \(root!.left.val)")       
            print("root.right = \(root!.right.val)")
            return 1
        }
        
    }

    Compile Error
    Line 18: Char 36: error: value of optional type 'TreeNode?' must be unwrapped to refer to member 'val' of wrapped base type 'TreeNode' in solution.swift
            print("root.left = \(root!.left.val)")       
                                    ^
    Line 19: Char 37: error: value of optional type 'TreeNode?' must be unwrapped to refer to member 'val' of wrapped base type 'TreeNode' in solution.swift
            print("root.right = \(root!.right.val)")
                                    ^




    需要加上驚嘆號


    class Solution {
        func findTilt(_ root: TreeNode?) -> Int {
            
            print("root.val = \(root!.val)")
            print("root.left = \(root!.left!.val)")       
            print("root.right = \(root!.right!.val)")
            return 1
        }
        
    }

    stdout
        root.val = 1
        root.left = 2
        root.right = 3

---

    class Solution {
        func findTilt(_ root: TreeNode?) -> Int {
            
            guard let leaf = root!.left else {
                return root!.val
            }
            
            // root. 
            
            let value = abs(findTilt(root!.left) - findTilt(root!.left))
            
            print("value = \(value)")
            return  value
        }
        
    }

    Wrong Answer
    Runtime: 12 ms
    Your input
    [1,2,3]
    stdout
    value = 0
    Output
    0
    Expected
    1

---
