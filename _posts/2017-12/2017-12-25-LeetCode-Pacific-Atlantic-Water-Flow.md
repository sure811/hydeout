---
layout: post
title: LeetCode - Pacific Atlantic Water Flow
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
Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.
<!--more-->

**Note:**
1. The order of returned grid coordinates does not matter.
2. Both m and n are less than 150.

**Example:**
```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```
### Java Solution
```java
static int[] dx = {-1,0,0,1};
static int[] dy = {0,1,-1,0};
public List<int[]> pacificAtlantic(int[][] matrix) {
    List<int[]> res = new ArrayList<>();
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return res;
    boolean[][] pacific = new boolean[matrix.length][matrix[0].length];
    boolean[][] atlantic = new boolean[matrix.length][matrix[0].length];
    for (int i = 0; i < matrix.length; i++){
        pacific[i][0] = true;
        atlantic[i][matrix[0].length-1] = true;
    }
    for (int j = 0; j < matrix[0].length; j++){
        pacific[0][j] = true;
        atlantic[matrix.length-1][j] = true;
    }
    for (int i = 0; i < matrix.length; i++){
        explore(pacific, matrix, i, 0);
        explore(atlantic, matrix, i, matrix[0].length-1);
    }
    for (int j = 0; j < matrix[0].length; j++){
        explore(pacific, matrix, 0, j);
        explore(atlantic, matrix, matrix.length-1, j);
    }
    for (int i = 0; i < matrix.length; i++){
        for (int j = 0; j < matrix[0].length; j++){
            if (pacific[i][j] && atlantic[i][j] == true)
                res.add(new int[]{i,j});
        }
    }
    return res;

}
private void explore(boolean[][] grid, int[][] matrix, int i, int j){
    grid[i][j] = true;
    for (int d = 0; d < dx.length; d++){
        if (i+dy[d] < grid.length && i+dy[d] >= 0 &&
            j + dx[d] < grid[0].length && j + dx[d] >= 0 &&
            grid[i+dy[d]][j+dx[d]] == false && matrix[i+dy[d]][j+dx[d]] >= matrix[i][j])
                explore(grid, matrix, i+dy[d], j+dx[d]);
    }
}
```