35. Search Insert Position
https://leetcode.com/problems/search-insert-position/


Given a sorted array and a target value, return the index if the target is found.   
If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:
>Input: [1,3,5,6], 5  
Output: 2  

Example 2:
>Input: [1,3,5,6], 2  
Output: 1

Example 3:
>Input: [1,3,5,6], 7  
Output: 4

Example 4:
>Input: [1,3,5,6], 0  
Output: 0

-----


成功的版本


``` 
int searchInsert(int* nums, int numsSize, int target){
    int lastGap = 0;
    int NowGap = 0;

    for(int i=0;i<numsSize;i++){
        NowGap = *(nums + i) - target;
        //printf("NowGap = %d \n",NowGap);
        if(NowGap == 0){
            return i;
        }
        if((lastGap<=0) && (NowGap >0)){
            return i;
        }
        lastGap = NowGap;

    }
   // printf("---------\n");
    return numsSize;
}
```

思路
依序將每一個元素 減去目標,觀察 差值的變化,思考邊界行為

他給的sample 給的很好
1. target  在array中找到相同的 --> 回傳那個數的index
2. target  比 array中的i-1位大  比i位小 --> 回傳 i 位
3. target  比 array中每一個都還小  所以得插入到最前面的位置 --> 0
4. target  比 array中每一個都還大  所以得插到最後面的下一個 --> numsSize
----
1. NowGap 為0
2. (lastGap < 0) && (NowGap >0)
3. (lastGap == 0) && (NowGap >0)
4. 上面for 都沒出來 就直接最後  return numsSize;
