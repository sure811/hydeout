---
layout: post
title: LeetCode - Set Matrix Zeroes
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
### My Java Solution
```java
public void setZeroes(int[][] matrix) {
    if(matrix.length == 0) return;
    for(int i = 0; i < matrix.length; i++){
        for(int j = 0; j < matrix[i].length; j++){
            if(matrix[i][j] == 0){
                matrix[i][0] = matrix[i][0] == 0 ? 0 : -255;
                matrix[0][j] = matrix[0][j] == 0 ? 0 : -255;
            }
        }
    }

    for(int i = 1; i < matrix.length || i < matrix[0].length; i++){
        if(i < matrix.length && (matrix[i][0] == 0 || matrix[i][0] == -255)){
            for(int j = 1; j < matrix[i].length; j++){
                matrix[i][j] = 0;
            }
        }
        if(i < matrix[0].length && (matrix[0][i] == 0 || matrix[0][i] == -255)){
            for(int j = 1; j < matrix.length; j++){
                matrix[j][i] = 0;
            }
        }
    }
    if(matrix[0][0] == 0){
        for(int i = 1; i < matrix.length; i++){
            matrix[i][0] = 0;
        }
        for(int i = 1; i < matrix[0].length; i++){
            matrix[0][i] = 0;
        }
    }
    else {
        boolean isZero = false;
        for(int i = 1; i < matrix.length; i++){
            if(matrix[i][0] == 0){
                isZero = true;
            }else if(matrix[i][0] == -255){
                matrix[i][0] = 0;
            }
        }
        if(isZero){
            for(int i = 0; i < matrix.length; i++){
                matrix[i][0] = 0;
            }
        }
        isZero = false;
        for(int i = 1; i < matrix[0].length; i++){
            if(matrix[0][i] == 0){
                isZero = true;
            }else if(matrix[0][i] == -255){
                matrix[0][i] = 0;
            }
        }
        if(isZero){
            for(int i = 0; i < matrix[0].length; i++){
                matrix[0][i] = 0;
            }
        }
    }
}
```
### Best Java Solution
```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        if(matrix==null){
            return;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        boolean rowHasZero = false;
        boolean colHasZero = false;

        for(int i=0; i<n; i++){
            if(matrix[0][i]==0){
                rowHasZero = true;
                break;
            }
        }

        for(int i=0; i<m; i++){
            if(matrix[i][0]==0){
                colHasZero = true;
                break;
            }
        }

        for(int i=1; i<m; i++){
            for(int j=1; j<n; j++){
                if(matrix[i][j]==0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }



        for(int j=1;j<n; j++){
            if(matrix[0][j]==0){
                nullifyCol(matrix, j, m, n);
            }
        }

        for(int i=1; i<m; i++){
            if(matrix[i][0]==0){
                nullifyRow(matrix, i, m, n);
            }
        }

        if(rowHasZero){
            nullifyRow(matrix, 0, m, n);
        }
        if(colHasZero){
            nullifyCol(matrix, 0, m, n);
        }

    }

    public void nullifyRow(int[][] matrix, int i, int m, int n){
        for(int col=0; col<n; col++){
            matrix[i][col] = 0;
        }
    }

    public void nullifyCol(int[][] matrix, int j, int m, int n){
        for(int row=0; row<m; row++){
            matrix[row][j] = 0;
        }
    }
}
```