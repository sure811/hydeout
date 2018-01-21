---
layout: post
title: LeetCode - Minimum Path Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.
<!--more-->

**Note:** You can only move either down or right at any point in time.

**Example 1:**
```
[[1,3,1],
 [1,5,1],
 [4,2,1]]
```
Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.
### My Java Solution
```java
public int minPathSum(int[][] grid) {
    if(grid.length == 0) return 0;
    int[][] dp = new int[grid.length + 1][grid[0].length + 1];
    for(int i = 1; i <= grid.length; i++){
        for(int j = 1; j <= grid[0].length; j++){
            if(i == 1)
                dp[i][j] = dp[i][j - 1] + grid[i - 1][j - 1];
            else if(j == 1)
                dp[i][j] = dp[i - 1][j] + grid[i - 1][j - 1];
            else
                dp[i][j] = Math.min(dp[i - 1][j] + grid[i - 1][j - 1], dp[i][j - 1] + grid[i - 1][j - 1]);
        }
    }
    return dp[grid.length][grid[0].length];
}
```