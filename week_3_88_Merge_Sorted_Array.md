88. Merge Sorted Array
https://leetcode.com/problems/merge-sorted-array/

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
---
[1,2,3,0,0,0]    3  
[2,5,6]  3  
nums1Size = 6   m = 3
nums2Size = 3   n = 3

觀察得到
  n == nums2Size
  m+n == nums1Size
---


  比較  兩個 array 的最前面

  把比較短的array
  將元素一個一個 到插入長的

  再長的中 找到比他大的 把他往後擠
  然後面每一個往後擠
  然後 直到  第二個元素能插入的位置   
  然後之後的 每個擠兩位


  思考  跑的方向性
  是不是先找大的比較好
  放到長的尾端
  感覺有m n
  就是為了從有意義的值 從大個開始找


  for nums1[]
