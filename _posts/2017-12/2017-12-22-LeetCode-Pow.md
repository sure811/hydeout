---
layout: post
title: LeetCode - Pow(x, n)
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

Implement pow(x, n).
<!--more-->

**Example 1:**
```
Input: 2.00000, 10
Output: 1024.00000
```
**Example 2:**
```
Input: 2.10000, 3
Output: 9.26100
```
### Java Solution
```java
public double myPow(double x, int n) {
    if(x == 1)
        return x;
    if(x == -1)
        return n % 2 == 0 ? 1: -1;
    if(n == Integer.MAX_VALUE || n == Integer.MIN_VALUE)
        return 0;
    if(n == 0)
        return 1;
    if(n<0){
        n = -n;
        x = 1/x;
    }
    return (n%2 == 0) ? myPow(x*x, n/2) : x*myPow(x*x, n/2);
}
```