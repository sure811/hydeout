---
layout: post
title: LeetCode - Ugly Number II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
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
    int[] res = new int[n];
    int pos2 = 0;
    int pos3 = 0;
    int pos5 = 0;
    res[0] = 1;
    for(int i = 1; i < n; i++){
        int temp = Math.min(Math.min(res[pos2] * 2, res[pos3] * 3), res[pos5] * 5);
        if(temp == res[pos2] * 2)
            pos2++;
        if(temp == res[pos3] * 3)
            pos3++;
        if(temp == res[pos5] * 5)
            pos5++;
        res[i] = temp;
    }

    return res[n - 1];
}
```