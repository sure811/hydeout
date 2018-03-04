---
layout: post
title: LeetCode - Divide Two Integers
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Divide two integers without using multiplication, division and mod operator.
<!--more-->

If it is overflow, return MAX_INT.
### Java Solution
```java
public int divide(int dividend, int divisor) {
    long m = Math.abs((long)dividend), n = Math.abs((long)divisor), res = 0;
    if (m < n) return 0;
    while (m >= n) {
        long t = n, p = 1;
        while (m > (t << 1)) {
            t <<= 1;
            p <<= 1;
        }
        res += p;
        m -= t;
    }
    if ((dividend < 0) ^ (divisor < 0)) res = -res;
    return res > Integer.MAX_VALUE ? Integer.MAX_VALUE : (int)res;
}
```