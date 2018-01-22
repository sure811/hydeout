---
layout: post
title: LeetCode - Game of Life
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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

**Follow up: **
1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

### My Java Solution
```java
public void gameOfLife(int[][] board) {
    for(int i = 0; i < board.length; i++){
        for(int j = 0; j < board[i].length; j++){
            int neighbors = 0;
            if(i > 0 && Math.abs(board[i - 1][j]) == 1)
                neighbors++;
            if(j > 0 && Math.abs(board[i][j - 1]) == 1)
                neighbors++;
            if(i > 0 && j > 0 && Math.abs(board[i - 1][j - 1]) == 1)
                neighbors++;
            if(i > 0 && j < board[i].length - 1 && Math.abs(board[i - 1][j + 1]) == 1)
                neighbors++;
            if(j < board[i].length - 1 && Math.abs(board[i][j + 1]) == 1)
                neighbors++;
            if(i < board.length - 1 && j < board[i].length - 1 && Math.abs(board[i + 1][j + 1]) == 1)
                neighbors++;
            if(i < board.length - 1 && j > 0 && Math.abs(board[i + 1][j - 1]) == 1)
                neighbors++;
            if(i < board.length - 1 && Math.abs(board[i + 1][j]) == 1)
                neighbors++;
            if(Math.abs(board[i][j]) == 1){
                if(neighbors < 2 || neighbors > 3)
                    board[i][j] = -1;
            } else {
                if(neighbors == 3)
                    board[i][j] = -2;
            }
        }
    }

    for(int i = 0; i < board.length; i++){
        for(int j = 0; j < board[i].length; j++){
            if(board[i][j] == -1)
                board[i][j] = 0;
            else if(board[i][j] == -2)
                board[i][j] = 1;
        }
    }
}
```