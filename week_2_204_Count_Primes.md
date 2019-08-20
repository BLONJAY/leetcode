## 嘗試 1. 一個一個去判斷  除以目前這個數 所有之前的數

## 嘗試 2. 創一個array,先存2  後續的數字去除以 array判斷是否為prime,是的話加入到array

## 嘗試 3. 多一個array 儲存 是否需要判斷
  * ### 創一個 size為 n 的 bool array,將全部初始化為true
  * ### 0 1 設為false
  * ### 2 判斷出來是prime  將所有2的倍數 設為 fasle,只有2是 true
  * ### 3 判斷出來是prime  將所有2的倍數 設為 fasle,只有3是 true
  * ### 4 因為是2的倍數,所以不用判斷
  * ### ....
  * ### 所以做後再跑一個for迴圈 判斷array中 true 的數量




``` c
// 找下一個未被刪掉的數字
for (int i=2; i<20000000; i++)
    if (prime[i])
        // 刪掉質數i的倍數，從兩倍開始。保留原本質數。
        for (int j=i+i; j<20000000; j+=i)
            prime[j] = false;
```

``` c
// 找下一個未被刪掉的數字
for (int i=2; i<20000000; i++)
    if (prime[i])
        // 刪掉質數i的倍數，從i倍開始。小心溢位。
        for (int j=i*i; j<20000000; j+=i)
            prime[j] = false;
```

``` c
for (int i=2; i<20000000; i++)
    if (prime[i])
        // k是倍率，j是質數i的倍數。
        // 由大到小判斷，當prime[k]成立時，
        // k才能涵蓋所有「大於等於i的質數、其倍數」倍。
        for (int k=(20000000-1)/i, j=i*k; k>=i; k--, j-=i)
            if (prime[k])
                prime[j] = false;
}
// 運用小範圍的prime[k]，避免存取大範圍的prime[j]，
// 大幅減少cache miss。

int countPrimes(int n){
    if((n == 0) || (n == 1))
        return 0;

    bool prime[n];


    for (int i=0; i<n; i++)
        prime[i] = true;

    prime[0] = false;
    prime[1] = false;

    for (unsigned long long i=2; i<n; i++){
        printf("prime[%d] = %d \n",i,prime[i]);
        if (prime[i])
            for (int k=(n-1)/i, j=i*k; k>=i; k--, j-=i){
                printf("      i = %d,k = %d, j =%d \n",i,k,j);
                printf("      prime[%d] = %d \n",k,prime[k]);
              if (prime[k])
                  printf("           prime[%d] 設為 false \n",j);
                 prime[j] = false;
            }
    }
    int primeCount = 0;
    for(int i=0;i<n;i++){
        if(prime[i]==true)    
            primeCount++;
    }   
    return primeCount;
}



prime[2] = 1
      i = 2,k = 9, j =18
      prime[9] = 1            prime[18] 設為 false
      i = 2,k = 8, j =16
      prime[8] = 1            prime[16] 設為 false
      i = 2,k = 7, j =14
      prime[7] = 1            prime[14] 設為 false
      i = 2,k = 6, j =12
      prime[6] = 1            prime[12] 設為 false
      i = 2,k = 5, j =10
      prime[5] = 1            prime[10] 設為 false
      i = 2,k = 4, j =8
      prime[4] = 1            prime[8] 設為 false
      i = 2,k = 3, j =6
      prime[3] = 1            prime[6] 設為 false
      i = 2,k = 2, j =4
      prime[2] = 1            prime[4] 設為 false
prime[3] = 1
      i = 3,k = 6, j =18
      prime[6] = 0
      i = 3,k = 5, j =15
      prime[5] = 1            prime[15] 設為 false
      i = 3,k = 4, j =12
      prime[4] = 0
      i = 3,k = 3, j =9
      prime[3] = 1            prime[9] 設為 false
prime[4] = 0
prime[5] = 1
prime[6] = 0
prime[7] = 1
prime[8] = 0
prime[9] = 0
prime[10] = 0
prime[11] = 1
prime[12] = 0
prime[13] = 1
prime[14] = 0
prime[15] = 0
prime[16] = 0
prime[17] = 1
prime[18] = 0
prime[19] = 1

```


## 嘗試紀錄

先用最笨的,如底下,結果超時

``` objc
int countPrimes(int n){
  int primeNumberCounter = 0;

  if(n<2){
    return primeNumberCounter;
  }

  for(int i=n-1;i>=2;i--){
    int divisibleCounter = 0;

    for(int j =i;j>=2;j--){
      if(i % (j-1)  == 0){
        divisibleCounter++;
      }
      if(j == 2){
        if(divisibleCounter == 1){
          primeNumberCounter++;
        }       
      }   
    }
  }
  return primeNumberCounter;
}
```
可能要使用 遞迴
或者去除偶數
或是一些質數的倍數  

目前我只適用最笨的方式
把輸入的n 一個一個 去除比他小的

可以換個方向  從小的 往大的判斷  
然後從/2 開始  然後慢慢紀錄 有的質數
然後較大的 就來除這些質數

這樣好像還是每一個要除  

但是應該比舊的好 舊的是雙重for


```objc
int countPrimes(int n){
  if(n<2){
    return 0;
  } else {
    // 想搞一個array 來存
    // 因為數字有一半是偶數  感覺開n/2就夠了
    // 是不是要用個 link list去給他長 最後回傳長度
    // 假設我們用array 要另一個 var 來記錄  

    int primeArray[n/2];

    for(int i=2;i<n;i++){
      if(i%2 == 0){

      }

    }
  }
  return primeNumberCounter;
}
```

底下的代碼會有這個問題

```
Line 16: Char 113: runtime error: index 50 out of bounds for type 'int [*]' (solution.c)
```

``` objc
int countPrimes(int n){
  int arrayLength = 1;

  if(n<2){
    return 0;
  } else {
    int primeArray[n/2];
    primeArray[0] = 2;

    for(int i=2; i<n; i++){
      for(int j=0; j<arrayLength; j++){
        if(i % primeArray[j] != 0){
          primeArray[arrayLength] = i;
          arrayLength++;
        }else{
          continue;
        }
      }
    }
  }
  return arrayLength;
}
```
