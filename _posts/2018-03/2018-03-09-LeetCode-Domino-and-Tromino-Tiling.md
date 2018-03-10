---
layout: post
title: LeetCode - Domino and Tromino Tiling
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
We have two types of tiles: a 2x1 domino shape, and an "L" tromino shape. These shapes may be rotated.
<!--more-->
```
XX  <- domino

XX  <- "L" tromino
X
```
Given N, how many ways are there to tile a 2 x N board? Return your answer modulo 10^9 + 7.

(In a tiling, every square must be covered by a tile. Two tilings are different if and only if there are two 4-directionally adjacent cells on the board such that exactly one of the tilings has both squares occupied by a tile.)
```
Example:
Input: 3
Output: 5
Explanation:
The five different ways are listed below, different letters indicates different tiles:
XYZ XXZ XYY XXY XYY
XYZ YYZ XZZ XYY XXY
```
**Note:**

* N  will be in range `[1, 1000]`.
### Java Solution
```java
public int numTilings(int N) {
    if(N < 2) return 1;
    int kMod = 1000000007;
    long[] dp = new long[N + 1];
    Arrays.fill(dp, 1);
    dp[2] = 2;
    for (int i = 3; i <= N; ++i)
      dp[i] = (dp[i - 3] + dp[i - 1] * 2) % kMod;
    return (int)dp[N];
}
```