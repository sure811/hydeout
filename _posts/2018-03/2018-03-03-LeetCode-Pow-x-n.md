---
layout: post
title: LeetCode - Pow(x, n)
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
public double myPow(double x, long n) {
    if(x == 1 || n == 0) return 1;
    if(n < 0) return 1 / myPow(x, -n);
    if(n == 1) return x;
    if(n % 2 == 0) {
        double half = myPow(x, n / 2);
        return half * half;
    }
    return myPow(x, n - 1) * x;
}
```