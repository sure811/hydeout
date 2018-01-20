---
layout: post
title: LeetCode -
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?
<!--more-->

Above is a 3 x 7 grid. How many possible unique paths are there?

**Note:** m and n will be at most 100.
### My Java Solution
```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for(int i = 0; i < m; i++){
        for(int j = 0; j < n; j++){
            if(i == 0 || j == 0) dp[i][j] = 1;
            else{
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }
    return dp[m - 1][n - 1];
}
```