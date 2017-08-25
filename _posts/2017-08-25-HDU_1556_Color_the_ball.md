---
layout: post
title: HDU 1556 Color the ball
date: 2017-08-25 
tag: HDU
---

题目链接：[HDU 1556 Color the ball](http://acm.hdu.edu.cn/showproblem.php?pid=1556)

-------------------
### 题面
* **Problem Description**

**N**个气球排成一排，从左到右依次编号为1,2,3....N.每次给定2个整数**a** **b**(a <= b),lele便为骑上他的“小飞鸽"牌电动车从气球a开始到气球b依次给每个气球涂一次颜色。但是N次以后lele已经忘记了第I个气球已经涂过几次颜色了，你能帮他算出每个气球被涂过几次颜色吗？

* **Input**

每个测试实例第一行为一个整数N,($N <= 100000$).接下来的N行，每行包括2个整数a b($1 <= a <= b <= N$)。
当N = 0，输入结束。

* **Output**

每个测试实例输出一行，包括N个整数，第I个数代表第I个气球总共被涂色的次数。

* **Sample Input**

3

1 1

2 2

3 3

3

1 1

1 2

1 3

0

* **Sample Output**

1 1 1

3 2 1

### 题意：

从1到N，每次给某区间涂色，求最后每个点涂色次数。 

### AC代码：
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

using namespace std;

int ans[1000005];
int n;

struct shu
{
    int l,r;
    int n;
}a[1000005];

void init(int l,int r,int i)
{
    a[i].l=l;
    a[i].r=r;
    a[i].n=0;
    if(l==r)
        return;
    int m=(l+r)>>1;
    init(l,m,i<<1);
    init(m+1,r,i<<1|1);
}

void update(int i,int x,int y)
{
    if(a[i].l==x&&a[i].r==y)
        a[i].n++;
    else
    {
        int m=(a[i].l+a[i].r)>>1;
        if(x>m)
            update(i<<1|1,x,y);
        else if(y<=m)
            update(i<<1,x,y);
        else
        {
            update(i<<1,x,m);
            update(i<<1|1,m+1,y);
        }
    }
}

void jisuan(int x)
{
    for(int i=a[x].l;i<=a[x].r;i++)
        ans[i]+=a[x].n;
    if(a[x].l==a[x].r)
        return;
    jisuan(x<<1);
    jisuan(x<<1|1);
}

int main()
{
    int x,y;
    while(~scanf("%d",&n),n)
    {
        init(1,n,1);
        memset(ans,0,sizeof ans);
        for(int i=0;i<n;i++)
        {
            scanf("%d%d",&x,&y);
            update(1,x,y);
        }
        jisuan(1);
        for(int i=1;i<n;i++)
            printf("%d ",ans[i]);
        printf("%d\n",ans[n]);
    }
    return 0;
}
```
