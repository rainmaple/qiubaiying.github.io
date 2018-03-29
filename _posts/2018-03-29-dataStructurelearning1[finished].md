
# 数据结构学习（一）
## 算法的定义
- 有限的指令集
- 产生输出
- 一定在有限的步骤之后终止
- 每一条指令必须
  - 充分明确的指标不可有歧义
  - 在计算机能处理的单位之内
  - 描述要抽象，不应依赖于任何一种计算机语言以及具体的实现手段
  - 如：选择排序的伪码描述

```
void selectionSort(int List[],int N)
{
  for(int i=0;i<N;i++)
  {
    MinPosition =ScanForMin(List,i,N-1);
  /* 从List[i]到List[N-1]中找到最小的元素，并将其位置赋给MinPostion：*/
    Swap(List[i],List[MinPosition]);
    /*将未排序部分的最小元素换到有序部分的最后位置；*/
  }
}
```

## 什么是好的算法
- 空间复杂度S(n)
>根据算法写成程序在执行时候占用的存储单元的长度。

备注：这个长度往往与输入数据的规模有关，而复杂度过高会造成内存使用超限进而程序中断

- 时间复杂度T(n)
>根据算法写成的程序在执行时耗费时间的长度。

这个长度往往也和输入数据的规模有关。时间复杂度过高会使得运行结果超时出现

#### Example关于递归调用的空间复杂度计算
```
void PrintN(int N)
{
  if(N)
  {
    PrintN(N-1);
    printf("%d\n",N);
  }
  return;
}

```

每调用一次PrintN就会在内存中占用一个用来记录程序段的内存单元线性增长故空间复杂度为S(N)=C*N，如下图：
![](https://www.supersuperhandsome.cn/assets/markdown-img-paste-2018032915095311.png)

#### Example关于多项式的运算的时间复杂度

```
//函数1
double f(int n,double a[],double x)
{
  int i;
  double p = a[0];
  for(i=1 ;i<=n;i++)
  {
    p+ =(a[i]*pow(x,i));
  }
  return p;
}

//函数2
double f (int n,double a[],double x)
{
  int i;
  double p=a[n];
  for(i=n;i>0;i--)
  {
    p=a[i-1]+x*p;
  }
  return p;
}
```

众所周知：执行加法的时间远远不及乘法
所以在此考虑时间复杂度的时候仅重视乘法；
函数1中使用了(1+2+3+...+n)=(n+1)n/2次乘法
而函数2中只用了n次乘法！！！

所以我们称函数1的时间复杂度为T(n)=C1n<sup>2</sup>+C2n
而函数2：T(n)=C1(n)
在分析一般算法的效率时，我们经常关注下面两种复杂度
- 最坏情况复杂度T<sub>worst</sub>(n)
- 平均复杂度T<sub>avg</sub>(n)

>通常我们不对算法做精细的分析而采用复杂度的渐进表示法

- T(n)=O(f(n))表示存在常数C>0,n<sub>0</sub>>0使得n>=n<sub>0</sub>时有T(n)<=C·f(n)
- T(n)=Ω(g(n))表示存在常数C>0,n<sub>0</sub>>0使得当n>=n0时有T(n)>=C·g(n)
- T(n)=θ(h(n))表示同时有T(n)=O(h(n))和T(n)=Ω(g(n)存在即同时有上界和下界

>复杂度的上界可以相对任意大而下界也可相对小，但是过大或者过小对于算法复杂的衡量没有意义一般取最为贴近的



>关于logn的说法，以什么为底数很重要么，只是差一个实属倍而已所以不必关注是什么底数，一般取2为底数

下面给出函数规模图
![](https://www.supersuperhandsome.cn/assets/markdown-img-paste-2018032920590053.png)


![](https://www.supersuperhandsome.cn/assets/markdown-img-paste-20180329210422697.png)
### 复杂度分析小技巧
- 若两段算法分别有复杂度T<sub>1</sub>(n)=O(f<sub>1</sub>(n))和T<sub>2</sub>O(f<sub>2</sub>(n))则

  - T<sub>1</sub>(n)+T<sub>2</sub>(n)=max(O(f<sub>1</sub>(n)),O(f<sub>2</sub>(n)))
  - T<sub>1</sub>(n)×T<sub>2</sub>(n)=O(f<sub>1</sub>(n)×f<sub>2</sub>(n))
- 若T(n)是关于n的k阶多项式，那么T(n)=θ(n<sup>k</sup>)
- for循环的时间复杂度等于循环次数乘以循环体代码的复杂度
- if-else结构的复杂度取决于if的条件判断复杂度和两个分支部分的复杂度，总体复杂度取三者中最大

### 实例

需求:要求函数f(i,j)=max{0,∑<sup>j</sup><sub>k=i</sub>A<sub>k</sub>}的最大值
```
int MaxSubseqSum1(int A[],int N){
  int ThisSum,MaxSum=0;
  int i,j,k;
  for(i=0;i<N;i++){
    for(j=i;j<N;j++){
      ThisSum=0;
      for(k=i;k<=j;k++){
        ThisSum+=A[k];
        if(ThisSum>MaxSum)
          MaxSum=ThisSum;
      }
    }
  }
}

```
上述代码算法复杂度为T(N)=O(N<sup>3</sup>)


```
//优化代码
int MxSubseqSum2(int A[],int N)
{
  int ThisSum，MaxSum=0;
  int i,j;
  for(i=0;i<N;i++)
  {
    ThisSum =0;
    for(j=i;j<N;j++)
    {
      ThisSum+=A[j];
      /*对相同的i不同的j只要在j-1循环的基础上累加1项即可*/
      if(ThisSum>MaxSum)
      {
        MaxSum=ThisSum;
      }
    }
  }

}
```
经过优化后T(N)=O(N<sup>2</sup>)
