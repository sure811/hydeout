---
layout: post
title: LeetCode - Ugly Number II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
<!--more-->

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.
### Java Solution
```java
public int nthUglyNumber(int n) {
    List<Integer> res = new LinkedList<>();
    res.add(1);
    int i2 = 0, i3 = 0, i5 = 0;
    while (res.size() < n) {
        int m2 = res.get(i2) * 2, m3 = res.get(i3) * 3, m5 = res.get(i5) * 5;
        int mn = Math.min(m2, Math.min(m3, m5));
        if (mn == m2) ++i2;
        if (mn == m3) ++i3;
        if (mn == m5) ++i5;
        res.add(mn);
    }
    return res.get(res.size() - 1);
}
```