---
layout: post
title: LeetCode - Minimum Path Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.
<!--more-->

**Example 1:**
```
[[1,3,1],
 [1,5,1],
 [4,2,1]]
 ```

Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.

### Java Solution (I)
```java
public int minPathSum(int[][] grid) {
    if(grid.length == 0)
        return 0;
    for(int i = 0; i < grid.length; i++){
        for(int j = 0; j < grid[i].length; j++){
            if(i == 0 && j == 0)
                continue;
            else if(i == 0)
                grid[i][j] = grid[0][j - 1] + grid[i][j];
            else if(j == 0)
                grid[i][j] = grid[i - 1][0] + grid[i][j];
            else
                grid[i][j] = Math.min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j];
        }
    }

    return grid[grid.length - 1][grid[0].length - 1];
}
```