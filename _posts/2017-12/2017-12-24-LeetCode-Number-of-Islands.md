---
layout: post
title: LeetCode - Number of Islands
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
    - Depth First Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.
<!--more-->

**Example 1:**
```
11110
11010
11000
00000
```
Answer: 1

**Example 2:**
```
11000
11000
00100
00011
```
Answer: 3
### Java Solution
```java
public int numIslands(char[][] grid) {
    int result = 0;
    for(int i = 0; i < grid.length; i++){
        for(int j = 0; j < grid[i].length; j++){
            if(grid[i][j] == '1'){
                result++;
                dfs(grid, i, j);
            }
        }
    }
    return result;
}

private void dfs(char[][] grid, int r, int c){
    int nr = grid.length;
    int nc = grid[0].length;

    if (r < 0 || c < 0 || r >= nr || c >= nc || grid[r][c] == '0') {
      return;
    }

    grid[r][c] = '0';
    dfs(grid, r - 1, c);
    dfs(grid, r + 1, c);
    dfs(grid, r, c - 1);
    dfs(grid, r, c + 1);

}
```