---
layout: post
title: 'hdu-3336 Count the string'
subtitle: 'next数组的妙用'
date: 2019-02-24
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 字符串
---

## [传送门](http://acm.hdu.edu.cn/showproblem.php?pid=3336)

## 题目描述

就是计算字符串中每一个前缀出现的次数，然后把这些次数给加起来就是答案，然后最后要把这个答案mod1007.

eg:对于字符串abab

它的前缀是a,ab,aba,abab

它们分别出现的次数为2,2,1,1

所以答案就是6

## 输入描述

第一行给一个T，代表有t组数据

接下来T个数据，首先会有一个数字n(1<=n<=200000),代表是字符串的长度

然后是一个字符串

## 输出

每个前缀出现次数之和再mod 10007

## 解题思路

```in
首先，我们可以确定的是每一个前缀至少出现了一次
然后，我们观察，对于那些不止一次过一次的前缀，他们必然会在之后的字符串中作为子串出现，准确的说，它会作为之后出现的子串的后缀出现
比如说aba
这里的a,就是作为aba的后缀出现。。。看到这里，是不是觉得想到了什么，前缀与后缀，自然就和next数组联系起来了,我们可以想一下next数组过程,是不是就大概明白了些呢，如果我们当前子串的next值不为0,那么就跳到它的前缀的位置那里去，直到遇到某一个串的next值为0,当然在这个过程中是要统计跳了多少次的，最后作为答案，注意取模
```

## code

 ```cpp
#include <bits/stdc++.h>
using namespace std;
#define r(x) x=read()
const int maxn=2e5+5;
int next[maxn];
inline int read(){
    int x=0,f=-1;
    char c=getchar();
    while(c<'0'||c>'9'){if(c=='-')f=-1;c=getchar();}
    while(c>='0'&&c<='9'){x=x*10+c-'0';c=getchar();}
    return x*f;
}
inline void next(string a)
{
   
    int i,j,len=a.size();
    next[0]=-1;
    k=-1;
    while(i<len)
    {
        if(k==-1||a[i]==a[k])
          {
               next[++i]=++k;
          }
        else k=next[k];
    }
}
int t,r;
int ans=0;
int len;
string str;
int main()
{
    r(t);
    while(t--)
    {
        ans=0;
        r(n);
        cin>>str;
        len=str.size();
        next(str);
        ans=0;
        for(i=1;i<len;i++)
        {
            int tmp=next[i];
            while(tmp!=0)
            {
                ans=(ans+1)%10007;
                tmp=next[tmp];
            }
        }
        cout<<(ans+len)%10007<<endl;
    }
    return 0;
}

 ```





 
