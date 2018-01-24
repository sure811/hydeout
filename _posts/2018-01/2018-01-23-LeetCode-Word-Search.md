---
layout: post
title: LeetCode - Word Search
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
<!--more-->

For example,
Given board =
```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.
### My Java Solution
```java
class Solution {
    int[] x = new int[]{0, -1, 1, 0};
    int[] y = new int[]{-1, 0, 0, 1};
    public boolean exist(char[][] board, String word) {
        if(board.length == 0 || board[0].length == 0) return false;
        boolean[][] visited = new boolean[board.length][board[0].length];
        for(int i = 0; i < board.length; i++)
            for(int j = 0; j < board[i].length; j++)
                if(board[i][j] == word.charAt(0)){
                    visited[i][j] = true;
                    if(exist(board, word, visited, i, j, 1))
                        return true;
                    visited[i][j] = false;
                }
        return false;
    }

    private boolean exist(char[][] board, String word, boolean[][] visited, int i, int j, int index){
        if(index == word.length()) return true;
        for(int k = 0; k < x.length; k++){
            if(i + x[k] >= 0 && i + x[k] < board.length && j + y[k] >= 0 && j + y[k] < board[i].length && !visited[i + x[k]][j + y[k]] && board[i + x[k]][j + y[k]] == word.charAt(index)){
                visited[i + x[k]][j + y[k]] = true;
                if(exist(board, word, visited, i + x[k], j + y[k], index + 1))
                    return true;
                visited[i + x[k]][j + y[k]] = false;
            }
        }
        return false;
    }
}
```