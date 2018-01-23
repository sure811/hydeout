---
layout: post
title: LeetCode - Unique Paths II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.
```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```
The total number of unique paths is 2.

**Note: **m and n will be at most 100.
### My Java Solution
```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    if(obstacleGrid.length == 0 || obstacleGrid[0].length == 0 || obstacleGrid[0][0] == 1)
        return 0;
    int[][] dp = new int[obstacleGrid.length + 1][obstacleGrid[0].length + 1];
    for(int i = 1; i < dp.length; i++){
        for(int j = 1; j < dp[i].length; j++){
            if(i == 1 && j == 1)
                dp[i][j] = 1;
            else if(obstacleGrid[i - 1][j - 1] == 1)
                dp[i][j] = 0;
            else{
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }
    return dp[obstacleGrid.length][obstacleGrid[0].length];
}
```