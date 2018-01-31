---
layout: post
title: LeetCode - 01 Matrix
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
Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.
<!--more-->

The distance between two adjacent cells is 1.
**Example 1:**
Input:
```
0 0 0
0 1 0
0 0 0
```
Output:
```
0 0 0
0 1 0
0 0 0
```
**Example 2:**
Input:
```
0 0 0
0 1 0
1 1 1
```
Output:
```
0 0 0
0 1 0
1 2 1
```

**Note:**
1. The number of elements of the given matrix will not exceed 10,000.
2. There are at least one 0 in the given matrix.
3. The cells are adjacent in only four directions: up, down, left and right.

### Java Solution
```java
public int[][] updateMatrix(int[][] matrix) {
    int m = matrix.length;
    int n = matrix[0].length;

    Queue<int[]> queue = new LinkedList<>();
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                queue.offer(new int[] {i, j});
            }
            else {
                matrix[i][j] = Integer.MAX_VALUE;
            }
        }
    }



    while (!queue.isEmpty()) {
        int[] cell = queue.poll();
        for (int[] d : dirs) {
            int r = cell[0] + d[0];
            int c = cell[1] + d[1];
            if (r < 0 || r >= m || c < 0 || c >= n ||
                matrix[r][c] <= matrix[cell[0]][cell[1]] + 1) continue;
            queue.add(new int[] {r, c});
            matrix[r][c] = matrix[cell[0]][cell[1]] + 1;
        }
    }

    return matrix;
}
```