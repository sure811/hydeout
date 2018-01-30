---
layout: post
title: LeetCode - Out of Boundary Paths
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
There is an m by n grid with a ball. Given the start coordinate (i,j) of the ball, you can move the ball to adjacent cell or cross the grid boundary in four directions (up, down, left, right). However, you can at most move N times. Find out the number of paths to move the ball out of grid boundary. The answer may be very large, return it after mod 109 + 7.
<!--more-->

**Example 1:**
```
Input:m = 2, n = 2, N = 2, i = 0, j = 0
Output: 6
Explanation:
```
**Example 2:**
```
Input:m = 1, n = 3, N = 3, i = 0, j = 1
Output: 12
Explanation:
```
**Note:**
1. Once you move the ball out of boundary, you cannot move it back.
2. The length and height of the grid is in range `[1,50]`.
3. N is in range `[0,50]`.
### Java Solution
```java
class Solution {
    int[] x = new int[]{-1, 0, 1, 0};
    int[] y = new int[]{0, -1, 0, 1};
    public int findPaths(int m, int n, int N, int _i, int _j) {
        double[][][] dp = new double[m][n][N + 1];
        for(int k = 1; k <= N; k++){
            for(int i = 0; i < m; i++){
                for(int j = 0; j < n; j++){
                    for(int l = 0; l < x.length; l++){
                        if(i + x[l] < 0 || i + x[l] >= m || j + y[l] < 0 || j + y[l] >= n)
                            dp[i][j][k]++;
                        else
                            dp[i][j][k] = (dp[i][j][k] + dp[i + x[l]][j + y[l]][k - 1]) % 1000000007;
                    }
                }
            }
        }
        return (int)(dp[_i][_j][N] % 1000000007);
    }
}
```