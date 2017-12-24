---
layout: post
title: LeetCode - Divide Two Integers
categories:
    - LeetCode
tags:
    - LeetCode
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
    if(dividend == Integer.MIN_VALUE && (divisor == 1 || divisor == -1)){
        return divisor == 1 ? Integer.MIN_VALUE : Integer.MAX_VALUE;
    }
    return (int)divideLong(dividend, divisor);
}

public long divideLong(long dd, long dv){
    boolean isPos = (dd > 0 && dv > 0) || (dd < 0 && dv < 0);
    dd = Math.abs(dd);
    dv = Math.abs(dv);
    int digits = 0;
    while(dv <= dd){
        dv <<= 1;
        digits++;
    }
    long res = 0;
    dv >>= digits;
    digits--;
    while(digits >= 0){
        if(dd >= (dv << digits)){
            dd -= dv << digits;
            res += 1 << digits;
        }
        digits--;
        System.out.println(res);
    }
    return isPos ? res : - res;
}
```