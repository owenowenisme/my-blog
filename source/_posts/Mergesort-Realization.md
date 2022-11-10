
---
title: Mergesort Realization
date: 2022-11-08 22:28:52
tags: code

---
# 前情提要

我知道網路上有一堆Mergesort的文章，寫的也比我好，但是因為我太菜了，不趁現在做一下筆記之後之後又要花時間理解🥵，然候順便讓我的文章看起來多一點也不錯。

---
# 觀念
Mergesort是基於分治衍伸出來的排序法，基本的觀念就是把一個陣列切成多塊排序，再合併起來的排序演算法（可以想成Sort and Merge?）。

而為什麼兩個排序好得陣列合併就是排序好的呢？
我們可以通過實際舉例來觀察：

現在有兩個陣列 \\(A=\\{1,3,5\\}\ , B=\\{2,4,6\\}\\)，皆已排序好。

Step 1:先比較兩陣列中最小的值：
　　\\(A[0]=1<B[0]=2\\)　　\\(1\\)比較小因此先填入
　　\\(Merged Array=\\{1\\}\\)
　　\\(Now:\ A[n]=\\{3,5\\}\ , B[n]=\\{2,4,6\\}\\)

Step 2:同上
　　\\(A[1]=3>B[0]=2\\)　　\\(2\\)比較小因此先填入
　　\\(Merged Array=\\{1,2\\}\\)
　　\\(Now:\ A[n]=\\{3,5\\}\ , B[n]=\\{4,6\\}\\)

Step N:重複以上步驟，若其中一個陣列已空，則直接把另一陣列所有值照順序填入。
　　\\(Merged Array=\\{1,2,3,4,5,6\\}\\)

可以發現Merged Array的數值已排序好！
並且總共操作了六次正好是我們所有的數值的數量，因此可以知道合併一次的時間複雜度為\\(O(n)\\)。
---
# 實作

```cpp
void mergesort(int l,int r){// l為左邊界 r右邊界 l到r為欲排序範圍
    if(l==r) 
        return;
    int mid=(l+r)/2;
    
    mergesort(l,mid);//拆成兩部分進行遞迴
    mergesort(mid+1,r);

    sortedmerge(l,r);//合併兩部分
}
```

``` cpp
void sortedmerged(int l,int r){
    int mid=(l+r)/2;
    for(int i=l,j=r,k=l;k<=r;k++){
        if(l<=mid&&(arr[i]<arr[j]||j>r)){
            tmp[k]=arr[i];//tmp陣列暫存
            i++;
        }
        else{
            tmp[k]=arr[j];
            j++;
        }
    }
    for(int i=l;i<=r;i++){
        arr[i]=tmp[i];//複製回原陣列
    }
}
```
# 時間複雜度 
如同前面敘述，合併一次要花費\\(O(n)\\)的時間，由於每次會分一半進行排序再合併因此會有\\(\log _{2} n\\)層。
因此，Mergesort的時間複雜度為\\(O(nlogn)\\)。



<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>