
283. Move Zeroes

https://leetcode.com/problems/move-zeroes/

```
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
```

思路一  
  遇到零  複製 下一位 來取代 這個 0  
  問題: 累計 兩個0 移動一位覆蓋就會有問題


---



某次submit  這個結果沒過

Input: [0,1,0]  
Output: [1,1,0]  
Expected: [1,0,0]

代碼:
``` 
void moveZeroes(int* nums, int numsSize){
    int  zeroCounts = 0;

    for(int i = 0; i < numsSize; i++){
         if( *(nums + i) == 0 ){
           zeroCounts++;
         } else {
           *(nums + i - zeroCounts) = *(nums + i);
         }

         if(i >= (numsSize - zeroCounts)){
              *(nums + i ) = 0;
         }
    }
}
```
---

最終解法
* for 一遍
* 遇到0 counter ＋１  
* 遇到非0 往前移動
* 非0數字 往前移的位數(目前的0數量 )
* 在從尾巴 for 一次 蓋上0
``` 
void moveZeroes(int* nums, int numsSize){
    int  zeroCounts = 0;

    for(int i = 0; i < numsSize; i++){
         if( *(nums + i) == 0 ){
            zeroCounts++;
         } else {
             *(nums + i - zeroCounts) = *(nums + i);
         }
    }
    while(zeroCounts > 0){
        *(nums+ numsSize - zeroCounts) = 0;
        zeroCounts--;
    }
}

```


另一種想法

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]

* 遇到０ 往右移 直到遇到0或者右邊底
* 遇到1  往左移 直到遇到1或者左邊底

---
另一種想法

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]

兩個指標
一個從左邊指 處理到哪邊了
愈0  swift直接 remove
一個記錄 移掉幾個0 最後屁股append

