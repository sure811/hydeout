---
layout: post
title: LeetCode - Perfect Squares
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

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.
<!--more-->

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.

### Java Solution I
```java
public int numSquares(int n) {
    while (n % 4 == 0) n /= 4;
    if (n % 8 == 7) return 4;
    for (int a = 0; a * a <= n; ++a) {
        int b = (int)Math.sqrt(n - a * a);
        if (a * a + b * b == n) {
            return (a > 0 ? 1 : 0) + (b > 0 ? 1 : 0);
        }
    }
    return 3;
}
```

### Java Solution II
```java
public int numSquares(int n) {
    int[] dp = new int[n + 1];
    for (int i = 0; i <= n; ++i) {
        dp[i] = Integer.MAX_VALUE;
    }
    dp[0] = 0;
    for (int i = 0; i <= n; ++i) {
        for (int j = 1; i + j * j <= n; ++j) {
            dp[i + j * j] = Math.min(dp[i + j * j], dp[i] + 1);
        }
    }
    return dp[n];
}
```