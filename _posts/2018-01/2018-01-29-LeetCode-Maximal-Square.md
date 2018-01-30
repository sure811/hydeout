---
layout: post
title: LeetCode - Maximal Square
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.
<!--more-->
For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 4.
### Java Solution
```java
public int maximalSquare(char[][] matrix) {
    if(matrix.length == 0) return 0;
    int[][] dp = new int[matrix.length][matrix[0].length];
    int max = 0;
    for(int i = 0; i < matrix.length; i++){
        for(int j = 0; j < matrix[i].length; j++){
            if(i == 0 || j == 0) dp[i][j] = matrix[i][j] == '1' ? 1 : 0;
            else if(matrix[i][j] == '0') dp[i][j] = 0;
            else {
                dp[i][j] = Math.max(1, 1 + Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])));
            }
            if(dp[i][j] > max) max = dp[i][j];
        }
    }
    return max * max;
}
```