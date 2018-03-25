---
layout: post
title: LeetCode - Bitwise AND of Numbers Range
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a range `[m, n]` where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.
<!--more-->

For example, given the range `[5, 7]`, you should return 4.
### Java Solution
```java
public int rangeBitwiseAnd(int m, int n) {
    int d = Integer.MAX_VALUE;
    while ((m & d) != (n & d)) {
        d <<= 1;
    }
    return m & d;
}
```