---
layout: post
title: LeetCode - Valid Sudoku
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

A partially filled sudoku which is valid.
<!--more-->
**Note:**
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.
### Java Solution
```java
public boolean isValidSudoku(char[][] board) {
    Map<Character, List<Integer[]>> map = new HashMap<>();

    for(int i = 0; i < board.length; i++){
        for(int j = 0; j < board[i].length; j++){
            char c = board[i][j];
            if(c == '.') continue;
            map.putIfAbsent(c, new LinkedList<>());
            for(Integer[] point : map.get(c)){
                if(point[0] == i || point[1] == j){
                    return false;
                }

                if((point[0] >= (i / 3) * 3 && point[0] < (i / 3 + 1) * 3)
                   && (point[1] >= (j / 3) * 3 && point[1] < (j / 3 + 1) * 3)){
                    return false;
                }
            }
            map.get(c).add(new Integer[]{i, j});
        }
    }
    return true;
}
```