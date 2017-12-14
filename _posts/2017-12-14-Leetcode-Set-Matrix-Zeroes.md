---
layout: post
title: LeetCode - Set Matrix Zeroes
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.
<!--more-->

**Follow up:**
Did you use extra space?
A straight forward solution using O(mn) space is probably a bad idea.
A simple improvement uses O(m + n) space, but still not the best solution.
Could you devise a constant space solution?

### Java Solution
```java
    public void setZeroes(int[][] matrix) {
        boolean iZero = false;
        for(int i = 0; i < matrix.length; i++){
            if(matrix[i][0] == 0){
                iZero = true;
                break;
            }
        }
        boolean jZero = false;
        for(int j = 0; j < matrix[0].length; j++){
            if(matrix[0][j] == 0){
                jZero = true;
                break;
            }
        }

        for(int i = 1; i < matrix.length; i++){
            for(int j = 1; j < matrix[i].length; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for(int i = 1; i < matrix.length; i++){
            for(int j = 1; j < matrix[i].length; j++){
                if (matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        if (iZero) {
            for (int i = 0; i < matrix.length; ++i) matrix[i][0] = 0;
        }
        if (jZero) {
            for (int i = 0; i < matrix[0].length; ++i) matrix[0][i] = 0;
        }
    }
```