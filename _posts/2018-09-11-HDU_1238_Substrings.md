---
layout: post
title: HDU 1238 Substrings(KMP)
date: 2018-09-11 
tag: HDU
---

题目链接：[HDU 1238 Substrings](http://acm.hdu.edu.cn/showproblem.php?pid=1238)

-------------------
### 题面
* **Problem Description**

You are given a number of case-sensitive strings of alphabetic characters, find the largest string **X**, such that either X, or its inverse can be found as a substring of any of the given strings.

* **Input**

The first line of the input file contains a single integer **t** ($1 <= t <= 10$), the number of test cases, followed by the input data for each test case. The first line of each test case contains a single integer **n** ($1 <= n <= 100$), the number of given strings, followed by n lines, each representing one string of minimum length 1 and maximum length 100. There is no extra white space before and after a string. 

* **Output**

There should be one line per test case containing the length of the largest string found. 

* **Sample Input**

2

3

ABCD

BCDFF

BRCD

2

rose

orchid

* **Sample Output**

2

2

### 题意

找出所有串最长的公共连续子串。 

### AC代码
``` c++
#include <bits/stdc++.h>

using namespace std;

void make_next(char *str,int *next,int l)
{
    next[0]=-1;
    int k=-1;
    for(int i=1;i<l;i++)
    {
        while(k>-1&&str[k+1]!=str[i])
            k=next[k];
        if(str[k+1]==str[i])
            k++;
        next[i]=k;
    }
}

bool KMP(char *str,int s_l,char *ptr,int p_l)
{
    int *next=new int[p_l];
    make_next(ptr,next,p_l);
    int k=-1;
    for (int i=0; i<s_l; i++)
    {
        while(k>-1&&ptr[k+1]!=str[i])
            k=next[k];
        if(ptr[k+1]==str[i])
            k++;
        if(k==p_l-1)
            return true;
    }
    return false;
}

void restr(char *x,char *y,int l)
{
    for(int i=0;i<=l;i++)
        y[i]=x[l-1-i];
    y[l]='\0';
}

int main()
{
    int t,min_l,minpos,ans;
    char s[105][105],s_f[105],s_temp[105],s_temp_re[105];
    bool flag;
    scanf("%d",&t);
    while(t--)
    {
        min_l=105;
        ans=0;
        int n;
        scanf("%d",&n);
        for(int i=0; i<n; i++)
        {
            scanf("%s",s[i]);
            if(min_l>strlen(s[i]))
            {
                min_l=strlen(s[i]);
                minpos=i;
            }
        }
        strcpy(s_f,s[minpos]);
        for(int i=0; i<min_l; i++)
        {
            for(int j=i+1; j<=min_l; j++)
            {
                if(j-i>ans)
                {
                    strncpy(s_temp,s_f+i,j-i);
                    s_temp[j-i]='\0';
                    s_temp_re[0]='\0';
                    restr(s_temp,s_temp_re,strlen(s_temp));
                    flag=true;
                    for(int k=0; k<n; k++)
                    {
                        if(k!=minpos)
                        {
                            if(!(KMP(s[k],strlen(s[k]),s_temp,strlen(s_temp))||KMP(s[k],strlen(s[k]),s_temp_re,strlen(s_temp_re))))
                            {
                                flag=false;
                                break;
                            }
                        }
                    }
                    if(flag)
                        ans=j-i;
                }
            }
        }
        printf("%d\n",ans);
    }
    return 0;
}
```
