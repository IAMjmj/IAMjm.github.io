---
layout: post
title: 'Ayoub and Lost Array '
subtitle: 'dp'
date: 2019-02-22
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: acm


---

## 

## [codeforce-1105c](http://codeforces.com/problemset/problem/1105/C)

## 题意

给定一个区间[l,r],用这里面的数组组成一个长度为n的数列，要求该数列之和是能被３整除，输出有多少种方案满足上面的条件，答案要mod(1e9+7);

## Input

The first and only line contains three integers n, l and r (1≤n≤2⋅105,1≤l≤r≤1091≤n≤2⋅105,1≤l≤r≤109) — the size of the lost array and the range of numbers in the array.

## Output

Print the remainder when dividing by 109+7 the number of ways to restore the array.

## 思路

对于这道题，看到的时候就完全不知道该怎么下下手，还是看的题解，

看完题解的话，又有点收获

第一,看到倍数的话可以往余数想，比如这里的3的倍数,就可以往%3想，记得上次也有一道类似的也是和这里的思路一样

第二，通常这种方案数的话，就是和dp联系起来;

题解上是这样写的，我先统计在[l,r]内%3==0的个数，%3==1的个数,%3==2的个数(用tot0,tot1,tot2来表示)

然后,我们再思考,该怎样表示状态，这里我们可能要用二维数组,```dp[maxn][maxn]``,第一维表示当前区间的长度

，第二维表示，当前区间总和%3==1,2,0的方案数

好了，这里我们再来思考一下动态转移方程，根据上面的状态，我们要求的是```dp[maxn][0]```

而这个状态肯定是从```dp[maxn-1][0~2]```转移而来，具体就是

```c++
dp[maxn-1][0]=(tot0*dp[maxn-1][0]+tot2*dp[maxn-1][1]+tot1*dp[maxn-1][2])%mod
dp[maxn-1][1]=(tot0*dp[maxn-1][1]+tot2*dp[maxn-1][2]+tot1*dp[maxn-1][0])%mod
dp[maxn-1][2]=(tot0*dp[maxn-1][2]+tot1*dp[maxn-1][1]+tot2*dp[maxn-1][0])%mod
这里需要自己想一下
```



## code

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const int mod=1e9+7
ll dp[100005][3];
int main()
{
    ll a,b,c,tot0,tot1,tot2;
    int i;
    int n,l,r;
    cin>>n>>l>>r;
    tot0=(r-l+1)/3;
    tot1=(r-l+1)/3
    tot2=(r-l+1)/3;
    for(i=0;i<(r-l+1)%3;i++)
    {
       if((l+i)%3==0)tot0++;
       if((l+i)%3==1)tot1++;
       if((l+i)%3==2)tot2++; 
    }
    dp[1][0]=tot0;
    dp[1][1]=tot1;
    dp[1][2]=tot2;
    for(i=2;i<=n;i++)
    {
       dp[i][0]=(dp[i-1][0]*tot0%mod+dp[i-1][1]*tot2%mod+dp[i-1][2]*tot1)%mod;
        dp[i][1]=(dp[i-1][1]*tot0%mod+dp[i-1][2]*tot2%mod+dp[i-1][0]*tot1)%mod;
        dp[i][2]=(dp[i-1][2]*tot0%mod+dp[i-1][0]*tot2%mod+dp[i-1][1]*tot1)%mod;
    }
    cout<<dp[n][0]<<endl;
    return 0;
}
```

