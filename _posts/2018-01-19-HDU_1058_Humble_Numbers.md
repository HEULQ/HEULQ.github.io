---
layout: post
title: HDU 1058 Humble Numbers（暴力）
date: 2018-01-19 
tag: HDU
---

题目链接：[HDU 1058 Humble Numbers](http://acm.hdu.edu.cn/showproblem.php?pid=1058)

-------------------
### 题面
* **Problem Description**

A number whose only prime factors are 2,3,5 or 7 is called a humble number. The sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 14, 15, 16, 18, 20, 21, 24, 25, 27, ... shows the first 20 humble numbers. 

Write a program to find and print the **n**th element in this sequence.

* **Input**

The input consists of one or more test cases. Each test case consists of one integer **n** with $1 <= n <= 5842$. Input is terminated by a value of zero (0) for n.

* **Output**

For each test case, print one line saying "The nth humble number is number.". Depending on the value of n, the correct suffix "st", "nd", "rd", or "th" for the ordinal number nth has to be used like it is shown in the sample output.

* **Sample Input**

1

2

3

4

11

12

13

21

22

23

100

1000

5842

0

* **Sample Output**

The 1st humble number is 1.

The 2nd humble number is 2.

The 3rd humble number is 3.

The 4th humble number is 4.

The 11th humble number is 12.

The 12th humble number is 14.

The 13th humble number is 15.

The 21st humble number is 28.

The 22nd humble number is 30.

The 23rd humble number is 32.

The 100th humble number is 450.

The 1000th humble number is 385875.

The 5842nd humble number is 2000000000.

### 题意

找出第N个Humble Number，定义是除1外所有仅有2,3,5,7因子的数。

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
#include <list>
#include <map>
#include <set>
#include <functional>

using namespace std;

int main()
{
    int n;
    long long s[6005];
    s[1]=1;
    int flag=1;
    int a=1,b=1,c=1,d=1;
    while(flag<=5842)
    {
        int min1=min(s[a]*2,s[b]*3);
        int min2=min(s[c]*5,s[d]*7);
        int minn=min(min1,min2);
        if(minn==s[a]*2)
            a++;
        else if(minn==s[b]*3)
            b++;
        else if(minn==s[c]*5)
            c++;
        else if(minn==s[d]*7)
            d++;
        if(s[flag]!=minn)
            s[++flag]=minn;
    }
    while(~scanf("%d",&n)&&n)
    {
        if(n%10==1&&n%100!=11)
            printf("The %dst humble number is ",n);
        else if(n%10==2&&n%100!=12)
            printf("The %dnd humble number is ",n);
        else if(n%10==3&&n%100!=13)
            printf("The %drd humble number is ",n);
        else
            printf("The %dth humble number is ",n);
        printf("%lld.\n",s[n]);
    }
    return 0;
}
```
