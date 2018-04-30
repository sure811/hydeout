---
layout: post
title: LeetCode - Surrounded Regions
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.
<!--more-->

For example,
```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```
### Java Solution
```java
class Solution {
    int[] dir_x = new int[]{0, -1, 0, 1};
    int[] dir_y = new int[]{-1, 0, 1, 0};
    public void solve(char[][] board) {
        if (board.length == 0) return;
        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (i == 0 || i == m - 1 || j == 0 || j == n - 1) {
                    if (board[i][j] == 'O') dfs(board, i , j);
                }
            }
        }
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == '$') board[i][j] = 'O';
            }
        }
    }
    void dfs(char[][] board, int x, int y) {
        int m = board.length, n = board[0].length;
        board[x][y] = '$';
        for (int i = 0; i < dir_x.length; ++i) {
            int dx = x + dir_x[i], dy = y + dir_y[i];
            if (dx >= 0 && dx < m && dy > 0 && dy < n && board[dx][dy] == 'O') {
                dfs(board, dx, dy);
            }
        }
    }
}
```