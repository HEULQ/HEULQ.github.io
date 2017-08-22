---
layout: post
title: XGDFZ Dynamic Programming Class 1st
date: 2017-01-05
tag: Class
---

### PDF
<iframe src="/pdf/XGDFZ16.12/XGDFZ16.12.22.pdf" style="width:100%; height:800px"></iframe>

### POJ 1745

<a target="_blank" href="http://poj.org/problem?id=1745"> Problem</a>  
Time Complexity: $O(N*K)$

{% highlight C++ %}

#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

const int maxn = 10005;
const int maxk = 105;

int f[maxn][maxk];
int n, K, A[maxn];

int main()
{
	cin >> n >> K;
	for (int i = 0; i < n; i++) {
		cin >> A[i];
		A[i] %= K;
		A[i] = (A[i] + K) % K;
	}
	memset(f, 0, sizeof(f));
	f[0][A[0]] = 1;
	for (int i = 1; i < n; i++) {
		for (int j = 0; j < K; j++) {
			f[i][j] = (f[i - 1][(j + A[i] + K) % K] | f[i - 1][(j - A[i] + K) % K]);
		}
	}
	if (f[n - 1][0])
		puts("Divisible");
	else
		puts("Not divisible");
	return 0;
}

{% endhighlight %}

### Codeforces 429B

<a target="_blank" href="http://codeforces.com/problemset/problem/429/B"> Problem</a>  

Only two possible cases are: Iahub comes from right, Iahubina comes from up or Iahub comes from down, Iahubina comes from right.
<dev align = "left">
  <img src="/images/posts/XGDFZ16.12/1.png" height="218" width="421">
</dev>
Then we can precalculate for dynamic programming matrixes.  
dp1[i][j] = maximal cost of a path going from (1, 1) to (i, j) only down and right.  
dp2[i][j] = maximal cost of a path from (i, j) to (n, m) going only down or right.  
dp3[i][j] = maximal cost of a path from (n, 1) to (i, j) going only up and right.  
dp4[i][j] = maximal cost of a path from (i, j) to (1, m) going only up and right.  
For details, plz refer to my code.  
Time Complexity: $O(N*M)$

{% highlight C++ %}

#include <bits/stdc++.h>
using namespace std;

const int maxn = 1005;

int n, m;
int dp1[maxn][maxn], dp2[maxn][maxn], dp3[maxn][maxn], dp4[maxn][maxn];
int A[maxn][maxn];

int main()
{
	cin >> n >> m;
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= m; j++)
			cin >> A[i][j];
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= m; j++)
			dp1[i][j] = A[i][j] + max(dp1[i - 1][j], dp1[i][j - 1]);
	for (int i = n; i >= 1; i--)
		for (int j = m; j >= 1; j--)
			dp2[i][j] = A[i][j] + max(dp2[i + 1][j], dp2[i][j + 1]);
	for (int i = n; i >= 1; i--)
		for (int j = 1; j <= m; j++)
			dp3[i][j] = A[i][j] + max(dp3[i][j - 1], dp3[i + 1][j]);
	for (int i = 1; i <= n; i++)
		for (int j = m; j >= 1; j--)
			dp4[i][j] = A[i][j] + max(dp4[i - 1][j], dp4[i][j + 1]);
	int ans = 0;
	for (int i = 2; i < n; i++)
		for (int j = 2; j < m; j++) {
			ans = max(ans, dp1[i][j - 1] + dp2[i][j + 1] + dp3[i + 1][j] + dp4[i - 1][j]); // first case
			ans = max(ans, dp1[i - 1][j] + dp2[i + 1][j] + dp3[i][j - 1] + dp4[i][j + 1]); // second case
		}
	cout << ans << endl;
	return 0;
}

{% endhighlight %}

### 2016 ACM-ICPC China-Final H
$$
\sum_{g=0}^{n*m}A_{g}*(g+1)=\sum_{g=0}^{min(n,m)}(A_{g}*g)+K^{n*m}=n*m*\sum_{i=2}^{K}((i-1)^{n + m - 2} * K^{n*m-n-m+1})
$$  
Time Complexity: $O(log_{2}n + log_{2}m)$
