---
layout: post
title: LeetCode - Minesweeper
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Let's play the minesweeper game (Wikipedia, online game)!

You are given a 2D char matrix representing the game board. 'M' represents an unrevealed mine, 'E' represents an unrevealed empty square, 'B' represents a revealed blank square that has no adjacent (above, below, left, right, and all 4 diagonals) mines, digit ('1' to '8') represents how many mines are adjacent to this revealed square, and finally 'X' represents a revealed mine.

Now given the next click position (row and column indices) among all the unrevealed squares ('M' or 'E'), return the board after revealing this position according to the following rules:

1. If a mine ('M') is revealed, then the game is over - change it to 'X'.
2. If an empty square ('E') with no adjacent mines is revealed, then change it to revealed blank ('B') and all of its adjacent unrevealed squares should be revealed recursively.
3. If an empty square ('E') with at least one adjacent mine is revealed, then change it to a digit ('1' to '8') representing the number of adjacent mines.
4. Return the board when no more squares will be revealed.
<!--more-->
**Example 1:**
```
Input:

[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

Output:

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

Explanation:
```
**Example 2:**
```
Input:

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

Click : [1,2]

Output:

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'X', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

Explanation:
```
Note:
1. The range of the input matrix's height and width is `[1,50]`.
2. The click position will only be an unrevealed square ('M' or 'E'), which also means the input board contains at least one clickable square.
3. The input board won't be a stage when game is over (some mines have been revealed).
4. For simplicity, not mentioned rules should be ignored in this problem. For example, you don't need to reveal all the unrevealed mines when the game is over, consider any cases that you will win the game or flag any squares.
### Java Solution
```java
class Solution {
    int[] left = {-1,0,1,-1,1,-1,0,1};
    int[] right = {-1,-1,-1,0,0,1,1,1};
    public char[][] updateBoard(char[][] board, int[] click) {
        if(board[click[0]][click[1]] == 'M')
        {
            board[click[0]][click[1]] = 'X';
            return board;
        }
        int count = 0;
        for(int i = 0; i < left.length; i++){
            if(click[0] + left[i] < board.length && click[0] + left[i] >= 0 && click[1] + right[i] < board[0].length && click[1] + right[i] >= 0 && board[click[0] + left[i]][click[1] + right[i]] == 'M')
                count++;
        }
        if(count > 0){
            board[click[0]][click[1]] = (char)('0' + count);
        }else{
            board[click[0]][click[1]] = 'B';
            for(int i = 0; i < left.length; i++){
                if(click[0] + left[i] < board.length && click[0] + left[i] >= 0 && click[1] + right[i] < board[0].length && click[1] + right[i] >= 0 && board[click[0] + left[i]][click[1] + right[i]] == 'E')
                    updateBoard(board, new int[]{click[0] + left[i], click[1] + right[i]});
            }
        }
        return board;
    }
}
```