---
layout: post
title: HDU 6143 Killer Names
date: 2017-08-22 
tag: HDU
---



$$
\sum_{i=1}^{min(m-1,n)}\Bigl((C_m^i*S_2(n,i)*i!)*(\sum_{j=1}^{min(m-i,n)}C_{m-i}^j*S_2(n,j)*j!)\Bigr)
$$




$$
\sum_{g=0}^{n*m}A_{g}*(g+1)=\sum_{g=0}^{min(n,m)}(A_{g}*g)+K^{n*m}=n*m*\sum_{i=2}^{K}((i-1)^{n + m - 2} * K^{n*m-n-m+1})
$$

$$
f(n) = \binom{m}{x} x^n - \sum_{1 \le i \lt n} \binom{n}{i} f(i)
$$
