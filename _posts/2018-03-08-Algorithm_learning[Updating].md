---
layout:     post
title: C++ DataStructrue Learning and Algorithm[personal]
subtitle:   学习
date:     2018-03-08
author:     TY
header-img: img/post-bg-DataStructrue.jpg
catalog: true
tags:
    - Algorithm_Learning
---

## C++数据结构与算法学习（一）
#### 前言
  最近在进行数据结构的学习，在了解了队列、堆栈、图等基础知识之后，决定去跟随潮流，一般来说大多数的程序员采用C++这门语言来进行基本算法的实现，但是由于自己的个人学习经历是从C到Java,因此对C++了解不深，接触之后发现爱上了这门语言感觉是C与Java的完美融合

#### 排序算法
#### 1. O(n^2)的排序算法
#### SelectionSort()选择排序
 简单叙述这个算法是：假设需求是将数组中的元素从小到大进行排列，那么我们首先需要做的就是将出数组中的第二元素开始到结尾的最小值，很熟悉的套路是遍历然后是同第一个交换，这样就保证了最小的排在了第一位，然后是寻找从第三个到结尾的数据集的最小值然后是同第二个交换依次类推。

#### 小小的总结：
 选择排序其实就是通过顺序遍历的方式选择元素，通过交换实现排序，这样的过程执行一次数组长度的遍历之后就完成了排序
 >评价：由于是经过大量的遍历与交换过程才实现排序，算法执行时间较慢

#### 代码：
  ```
    ///选择排序
    template<typename T>

    void selectionSort(T arr[],int n){
      for(int i=0;i<n;i++){
          //选择[i,n)ֵ最小的
          int minIndex=i;
          for(int j=i+1;j<n;j++){
              if(arr[j]<arr[minIndex]){
                  minIndex=j;
                }
                swap(arr[i],arr[minIndex]);
              }
          }
      }
  ```

#### InsertionSort()插入排序
经典的对于这个算法的描述是类比插扑克牌从而理顺手中牌的方法，我认为如果仅仅这样理解插入排序缺了几分深度和考究。首先还是以arr[n]举例。同样是假定遵守升序规律，我们从手中的arr[1]即第二张牌开始，先和前面一张牌arr[0]进行比较,小的话则进行交换，那么我们需要做的就是将数组中的第二元素开始的其他元素比如arr[i]按照顺序依次和前面的元素进行比较，遍历一直进行到找到前面的数（比入如arr[j]）比arr[i]还要小，此时该元素的排序遍历过程立即结束，开始进行该元素arr[i]同arr[j]交换,当所有的元素完成这样的交换遍历过程后则完成插入排序。

#### 小小的总结：
插入排序在于在将无顺序集合的第一个元素通过比较插入有序集合从而实现排序。
 > 评价:由于在算法实现时候遍历的终止条件多，可能先停下遍历查找的几率大，所以相对于选择排序在大数据集合的排序过程表现会相对优异

#### 代码实现

   ```
    //插入排序C++函数编写
    template<typename T>
    void insertionSort(T arr[], int n){
      for(int i=0;i<n;i++){
        for(int j=i;j>0;j--){
            if(arr[j]<arr[j-1]){
              swap(arr[i],arr[i-1]);
            }
            else break;
        }    
      }
    }  
   ```
#### 关于插入排序算法的优化
由于插入排序中涉及swap交换，拥有基础编程经验的码友们都知道，一次交换就涉及到三次赋值例如temp=a[i];->a[i]=a[j];->a[j]=temp;这样就会使得运算的时间变大,但是如果我们的算法只是用赋值来实现...

#### 代码实现

 ```
  template<typename T>
  void insertionSortOp(T arr[],int[] n){
    for(int i=0;i<n;i++){
      //e代表需要排序的元素，先对它进行个备份
      T e =arr[i];
      //j保存元素e应该插入的位置
      int j;
      for(j=i;j>0&&a[j-1]>e;j--){//终止的条件是找到要插入的位置的前一位比e小
        arr[j]=a[j-1];//后移一位腾位置
      }
      arr[j] = e;
    }
  }
  ```

![思路演示](https://www.supersuperhandsome.cn/assets/InsertionSortOP.gif)

#### 选择排序、插入排序、优化后的算法比较
随机产生一个数据集合，然后拷贝三份，比较三种算法算法对于统一数据集的排序时间效率比较

![结果演示](https://www.supersuperhandsome.cn/assets/markdown-img-paste-20180308202919285.png)
You can get my code from my [Github](https://github.com/rainmaple/Algorithm_Learning)
