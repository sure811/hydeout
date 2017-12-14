---
layout: post
title: LeetCode - Game of Life
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population..
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

Write a function to compute the next state (after one update) of the board given its current state.
<!--more-->

**Follow up: **

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

### Java Solution
```java
    public void gameOfLife(int[][] board) {
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                int sum = 0;
                sum += (i == 0 ? 0 : board[i - 1][j] % 2);
                sum += (j == 0 ? 0 : board[i][j - 1] % 2);
                sum += (i == 0 || j == 0 ? 0 : board[i - 1][j - 1] % 2);
                sum += (i == board.length - 1 ? 0 : board[i + 1][j] % 2);
                sum += (j == board[i].length - 1 ? 0 : board[i][j + 1] % 2);
                sum += (i == board.length - 1 || j == board[i].length - 1 ? 0 : board[i + 1][j + 1] % 2);
                sum += (i == 0 || j == board[i].length - 1 ? 0 : board[i - 1][j + 1] % 2);
                sum += (i == board.length - 1 || j == 0 ? 0 : board[i + 1][j - 1] % 2);
                if(board[i][j] == 1){
                    if(sum < 2)
                        board[i][j] = 1;
                    else if(sum == 2 || sum == 3)
                        board[i][j] = 3;
                    else if(sum > 3)
                        board[i][j] = 1;
                }else{
                    if(sum == 3)
                        board[i][j] = 2;
                }
            }
        }

        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                board[i][j] = board[i][j] / 2;
            }
        }
    }
```
