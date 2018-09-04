---
layout: post
title: HDU 4372 Count the buildings（第一类斯特林数）
date: 2017-08-23 
tag: HDU
---

题目链接：[HDU 4372 Count the buildings](http://acm.hdu.edu.cn/showproblem.php?pid=4372)

-------------------
### 题面
* **Problem Description**

There are **N** buildings standing in a straight line in the City, numbered from 1 to N. The heights of all the buildings are distinct and between 1 and N. You can see **F** buildings when you standing in front of the first building and looking forward, and **B** buildings when you are behind the last building and looking backward. A building can be seen if the building is higher than any building between you and it. 
Now, given N, F, B, your task is to figure out how many ways all the buildings can be.

* **Input**

 First line of the input is a single integer **T** ($T<=100000$), indicating there are T test cases followed. 
Next T lines, each line consists of three integer **N**, **F**, **B**, ($0<N, F, B<=2000$) described above.

* **Output**

For each case, you should output the number of ways mod 1000000007(1e9+7).

* **Sample Input**

2

3 2 2

3 2 1

* **Sample Output**

2

1

### 题意

n个房子在一条线上($n<=2000$)，高度分别为1~n，现在需要将房子这样放置：从最左往右能看到F个房子，从最右往左能看到B个房子，能看到的条件是：两者之间的房子都要低于这个房子。问这样的方案数。 

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
#define MOD 1000000007

using namespace std;

long long s1[2005][2005];
long long c[2005][2005];

void stirling_and_C()
{
    for(int i=1; i<=2002; i++)
    {
        c[0][0]=1;
        c[i][0]=c[i][i]=1;
        s1[i][0]=0;
        s1[i][i]=1;
        for(int j=1; j<i; j++)
        {
            c[i][j]=(c[i-1][j]+c[i-1][j-1])%MOD;
            s1[i][j]=(s1[i-1][j-1]+(i-1)*s1[i-1][j])%MOD;
        }
    }
}

int main()
{
    int t;
    scanf("%d",&t);
    stirling();
    while(t--)
    {
        int n,f,b;
        scanf("%d%d%d",&n,&f,&b);
        if(f+b-2>n)
        {
            printf("0\n");
            continue;
        }
        printf("%d\n",(c[f+b-2][f-1]*s1[n-1][f+b-2])%MOD);
    }
    return 0;
}
```
