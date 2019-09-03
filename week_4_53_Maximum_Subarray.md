int maxSubArray(int* nums, int numsSize){

    bool combine = false;
    int result = *nums;

    for(int i =1; i<numsSize; i++){
        if((*(nums + i) > 0) && (*(nums + i-1) < 0)){
            if(result < 0){
                result = 0;
            }
        }
        result += *(nums + i);
        printf("%d ",result);

    }

    return result;
}



// 負 下一個正  總結目前加總  如果為負 歸零
// 其餘一直加
// 問題
// [-2,1,-3,4,-1,2,1,-5,4]
//     1 -2 4  3 5 6  1 5

------------------
//  想法 找一個存最大值
//  然後順便避免  全負的


int maxSubArray(int* nums, int numsSize){

    bool combine = false;
    int tempHigh = *nums;
    int totalHigh = *nums;

    for(int i =1; i<numsSize; i++){
        if((*(nums + i) > 0) && (*(nums + i-1) < 0)){
            if(tempHigh < 0){
                tempHigh = 0;
            }
        }
        tempHigh += *(nums + i);

        if (totalHigh < tempHigh)
               totalHigh = tempHigh;

        if (totalHigh < *(nums + i))
               totalHigh = *(nums + i);
    }

    return totalHigh;
}

倒在這個

[0,-3,-1,0,2,3,-3]
因為沒遇到正的
發現不是因為尾端沒遇到正的
是因為 -1 遇到0  沒在我的負轉正
(*(nums + i) >= 0)

改完如下

int maxSubArray(int* nums, int numsSize){

    bool combine = false;
    int tempHigh = *nums;
    int totalHigh = *nums;

    for(int i =1; i<numsSize; i++){
        if((*(nums + i) >= 0) && (*(nums + i-1) < 0)){
            if(tempHigh < 0){
                tempHigh = 0;
            }
        }
        tempHigh += *(nums + i);

        if (totalHigh < tempHigh)
               totalHigh = tempHigh;

        if (totalHigh < *(nums + i))
               totalHigh = *(nums + i);

       // printf(" temp %d  total %d \n",tempHigh,totalHigh);
    }

    return totalHigh;
}



Runtime: 8 ms, faster than 69.46% of C online submissions for Maximum Subarray.
Memory Usage: 7.5 MB, less than 94.74% of C online submissions for Maximum Subarray.




-------
別人的做法
(tmpCnt + nums[i]) < nums[i])

適核心的思緒 差異

我是遇到負 正  才處理,  而且是判斷 tmp < 0


他們是tmp 加 目前  小於自己

```
int maxSubArray(int* nums, int numsSize){
    int totalCnt = nums[0];
    int tmpCnt = nums[0];
    for (int i = 1; i < numsSize; i++) {
        if ((tmpCnt + nums[i]) < nums[i]) {
            tmpCnt = 0;
        }
        tmpCnt += nums[i];
        if (totalCnt < tmpCnt) {
            totalCnt = tmpCnt;
        }
    }
    return totalCnt;
}
```



int maxSubArray(int* nums, int numsSize){
    int max_sum;
    int sum = 0;
    int i;

    if (!numsSize)
        return 0;

    max_sum = nums[0];
    for (i = 0; i < numsSize; i++) {
        sum += nums[i];
        max_sum = fmax(max_sum, sum);
        sum = fmax(0, sum);
    }
    return max_sum;
}
