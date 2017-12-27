---
layout: post
title: LeetCode - Out of Boundary Paths
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
There is an m by n grid with a ball. Given the start coordinate (i,j) of the ball, you can move the ball to adjacent cell or cross the grid boundary in four directions (up, down, left, right). However, you can at most move N times. Find out the number of paths to move the ball out of grid boundary. The answer may be very large, return it after mod 109 + 7.
<!--more-->

**Example 1:**
Input:m = 2, n = 2, N = 2, i = 0, j = 0
Output: 6
Explanation:

**Example 2:**
Input:m = 1, n = 3, N = 3, i = 0, j = 1
Output: 12
Explanation:

Note:
1. Once you move the ball out of boundary, you cannot move it back.
2. The length and height of the grid is in range `[1,50]`.
3. N is in range `[0,50]`.
### Java Solution
```java
public int findPaths(int m, int n, int N, int i, int j) {
    long[][][] dp = new long[N + 1][m][n];
    for (int k = 1; k <= N; ++k) {
        for (int x = 0; x < m; ++x) {
            for (int y = 0; y < n; ++y) {
                long v1 = (x == 0) ? 1 : dp[k - 1][x - 1][y];
                long v2 = (x == m - 1) ? 1 : dp[k - 1][x + 1][y];
                long v3 = (y == 0) ? 1 : dp[k - 1][x][y - 1];
                long v4 = (y == n - 1) ? 1 : dp[k - 1][x][y + 1];
                dp[k][x][y] = (v1 + v2 + v3 + v4) % 1000000007;
            }
        }
    }
    return (int)dp[N][i][j];
}
```