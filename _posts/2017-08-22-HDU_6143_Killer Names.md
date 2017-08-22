---
layout: post
title: HDU 6143 Killer Names
date: 2017-08-22 
tag: HDU
---

#Killer Names

*Time Limit: 2000/1000 MS (Java/Others)    Memory Limit: 65536/65536 K (Java/Others)*
*Total Submission(s): 1150    Accepted Submission(s): 567*


**Problem Description**
> Galen Marek, codenamed Starkiller, was a male Human apprentice of the Sith Lord Darth Vader. A powerful Force-user who lived during the era of the Galactic Empire, Marek originated from the Wookiee home planet of Kashyyyk as the sole offspring of two Jedi Knights—Mallie and Kento Marek—who deserted the Jedi Order during the Clone Wars. Following the death of his mother, the young Marek's father was killed in battle by Darth Vader. Though only a child, Marek possessed an exceptionally strong connection to the Force that the Dark Lord of the Sith sought to exploit.
>
> When Marek died in 2 BBY, shortly after the formation of the Alliance, Vader endeavored to recreate his disciple by utilizing the cloning technologies of the planet Kamino. The accelerated cloning process—an enhanced version of the Kaminoan method which allowed for a rapid growth rate within its subjects—was initially imperfect and many clones were too unstable to take Marek's place as the Dark Lord's new apprentice. After months of failure, one particular clone impressed Vader enough for him to hope that this version might become the first success. But as with the others, he inherited Marek's power and skills at the cost of receiving his emotions as well, a side effect of memory flashes used in the training process.
>
> — Wookieepedia

Darth Vader is finally able to stably clone the most powerful soilder in the galaxy: the Starkiller. It is the time of the final strike to destroy the Jedi remnants hidden in every corner of the galaxy.

However, as the clone army is growing, giving them names becomes a trouble. A clone of Starkiller will be given a two-word name, a first name and a last name. Both the first name and the last name have exactly n characters, while each character is chosen from an alphabet of size m. It appears that there are m2n possible names to be used.

Though the clone process succeeded, the moods of Starkiller clones seem not quite stable. Once an unsatisfactory name is given, a clone will become unstable and will try to fight against his own master. A name is safe if and only if no character appears in both the first name and the last name.

Since no two clones can share a name, Darth Vader would like to know the maximum number of clones he is able to create.
 

**Input**
The First line of the input contains an integer T (T≤10), denoting the number of test cases. 

Each test case contains two integers n and m (1≤n,m≤2000).
 

**Output**
For each test case, output one line containing the maximum number of clones Vader can create.

Output the answer  mod 109+7
 

**Sample Input**
2
3 2
2 3
 

**Sample Output**
2 
18
 
----------

前几天多校的题目，貌似还是个签到题？？？

**题意：**
两个长度为 n 的字符串（first name & last name），给你 m 个字母。在 first name 和 last name 中没有重复的字母，字母可重复使用，问有多少种可能情况。
我的思路是先选一些字母给 first name，再在剩下的字母中选一些给 last name，这样一共有

$$\bigl(\sum_{i=1}^{min(m-1,n)}C_m^i\bigr)*\bigl(\sum_{j=1}^{min(m-i,n)}C_{m-i}^j\bigr)$$

种分配方法。
接下来要考虑的问题就是 x 个字母怎样组成一个长度为 n 的字符串。
我想到的是第二类斯特林数，把长度为 n 的字符串想成 n 个格子，把这些格子分给 x 个字母，再对 x 个字母进行全排列。这样得到的就是 $S_2(n,x)*x!$ 

种方案。
整理一下：

$$\sum_{i=1}^{min(m-1,n)}\Bigl((C_m^i*S_2(n,i)*i!)*(\sum_{j=1}^{min(m-i,n)}C_{m-i}^j*S_2(n,j)*j!)\Bigr)$$


代码如下：
```c++
#include<stdio.h>
#include<memory.h>
#define maxn 2005
#define mod 1000000007
#define ll long long
ll s[maxn][maxn];
ll c[maxn][maxn];
ll a[maxn];
void init()
{
    int i,j;

    memset(s,0,sizeof(s));
    memset(c,0,sizeof(c));

    for(i=0;i<maxn;i++) c[i][0]=1;
    for(i=1;i<maxn;i++)
    for(j=1;j<maxn;j++)
    {
        c[i][j]=(c[i-1][j]+c[i-1][j-1])%mod;
    }

    for(i=0;i<maxn;i++)
    {
        s[i][0]=0;
        s[i][1]=1;
        s[i][i]=1;
    }
    for(i=2;i<maxn;i++)
    {
        for(j=i-1;j>1;j--)
             s[i][j]=(s[i-1][j-1]+j*s[i-1][j])%mod;
    }

    for(i=1;i<maxn;i++)
    {
        a[i]=1;
        for(j=i;j>0;j--)
            a[i]=(a[i]*j)%mod;
    }

    return ;
}

int main()
{
    init();
    int t;
    scanf("%d",&t);
    while(t--)
    {
        int n,m;
        scanf("%d %d",&n,&m);
        int i,j;
        ll res=0;
        for(i=1;i<=((m-1)<n?(m-1):n);i++)
        {
            int what=0;
            for(j=1;j<=((m-i)<n?(m-i):n);j++)
            {
                what=(what+(((c[m-i][j]*s[n][j])%mod)*a[j])%mod)%mod;
            }
            res=(res+(((((what*c[m][i])%mod)*s[n][i])%mod)*a[i])%mod)%mod;
        }
        printf("%lld\n",res);
    }
}
```
----------

**多校的题解：**
利用容斥原理计数. 设长度为 nn, 恰好用了 xx 个字符的方案数为 f(n)f(n), 那么

$$f(n) = \binom{m}{x} x^n - \sum_{1 \le i \lt n} \binom{n}{i} f(i)$$

好……好厉害的公式……

----------

P.S.
第一次用*markdown*，还不是很熟练，公式可能有错的地方请勿深究。
