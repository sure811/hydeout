---
layout: post
title: LeetCode - Pacific Atlantic Water Flow
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
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
public List<int[]> pacificAtlantic(int[][] matrix) {
    List<int[]> result = new LinkedList<>();
    if (matrix.length == 0) return result;
    int m = matrix.length, n = matrix[0].length;
    boolean[][] pacific = new boolean[m][n];
    boolean[][] atlantic = new boolean[m][n];
    for (int i = 0; i < m; ++i) {
        dfs(matrix, pacific, Integer.MIN_VALUE, i, 0);
        dfs(matrix, atlantic, Integer.MIN_VALUE, i, n - 1);
    }
    for (int i = 0; i < n; ++i) {
        dfs(matrix, pacific, Integer.MIN_VALUE, 0, i);
        dfs(matrix, atlantic, Integer.MIN_VALUE, m - 1, i);
    }
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (pacific[i][j] && atlantic[i][j]) {
                result.add(new int[]{i, j});
            }
        }
    }
    return result;
}
void dfs(int[][] matrix, boolean[][] visited, int pre, int i, int j) {
    int m = matrix.length, n = matrix[0].length;
    if (i < 0 || i >= m || j < 0 || j >= n || visited[i][j] || matrix[i][j] < pre) return;
    visited[i][j] = true;
    dfs(matrix, visited, matrix[i][j], i + 1, j);
    dfs(matrix, visited, matrix[i][j], i - 1, j);
    dfs(matrix, visited, matrix[i][j], i, j + 1);
    dfs(matrix, visited, matrix[i][j], i, j - 1);
}
```