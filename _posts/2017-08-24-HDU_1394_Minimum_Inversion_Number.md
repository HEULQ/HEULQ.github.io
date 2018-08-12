---
layout: post
title: HDU 1394 Minimum Inversion Number
date: 2017-08-24 
tag: HDU
---

题目链接：[HDU 1394 Minimum Inversion Number](http://acm.hdu.edu.cn/showproblem.php?pid=1394)

-------------------
### 题面
* **Problem Description**

The inversion number of a given number sequence $a_1$, $a_2$, ..., $a_n$ is the number of pairs ($a_i$, $a_j$) that satisfy i < j and $a_i$ > $a_j$.

For a given sequence of numbers $a_1$, $a_2$, ..., $a_n$, if we move the first m >= 0 numbers to the end of the seqence, we will obtain another sequence. There are totally **n** such sequences as the following:

$a_1$, $a_2$, ..., $a_{n-1}$, $a_n$ (where m = 0 - the initial seqence)

$a_2$, $a_3$, ..., $a_n$, $a_1$ (where m = 1)

$a_3$, $a_4$, ..., $a_n$, $a_1$, $a_2$ (where m = 2)

...

$a_n$, $a_1$, $a_2$, ..., $a_{n-1}$ (where m = n-1)

You are asked to write a program to find the minimum inversion number out of the above sequences.

* **Input**

The input consists of a number of test cases. Each case consists of two lines: the first line contains a positive integer n ($n <= 5000$); the next line contains a permutation of the n integers from 0 to n-1.

* **Output**

For each case, output the minimum inversion number on a single line.

* **Sample Input**

10

1 3 6 9 0 8 5 7 4 2

* **Sample Output**

16

### 题意

一个由0..n-1组成的序列，每次可以把队首的元素移到队尾，求形成的n个序列中最小逆序对数目 

### AC代码
``` c++
#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>
#include <algorithm>
#include <iostream>
#include <locale>
#include <vector>
#include <string>
#include <iomanip>
#include <cstdio>
#include <cstring>
#include <stack>
#include <queue>
#include <map>
#include <set>
#include <functional>
#define maxn 100007

using namespace std;

int main()
{
    int n;
    int a[5005];
    while(~scanf("%d",&n))
    {
        long long minn=0;
        for(int i=0;i<n;i++)
        {
            scanf("%d",&a[i]);
            for(int j=0;j<i;j++)
            {
                if(a[j]>a[i])
                    minn++;
            }
        }
        long long ans=minn;
        for(int i=0;i<n;i++)
        {
            ans=ans+n-2*a[i]-1;
            if(ans<minn)
                minn=ans;
        }
        printf("%lld\n",minn);
    }
    return 0;
}
```
