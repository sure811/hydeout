---
layout: post
title: LeetCode - Rotate Image
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).
<!--more-->

**Note:**
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

**Example 1:**
```
Given input matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```
**Example 2:**
```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```
### My Java Solution
```java
class Solution {
    public void rotate(int[][] matrix) {
        rotate(matrix, 0, 0, matrix.length);
    }

    private void rotate(int[][] matrix, int startX, int startY, int length){
        if(length == 1) return;

        for(int i = 0; i < length / 2; i++){
            for(int j = 0; j < length / 2; j++){
                int temp = matrix[startX + i][startY + j];
                matrix[startX + i][startY + j] = matrix[startX + length - length / 2 + i][startY + j];
                matrix[startX + length - length / 2 + i][startY + j] = matrix[startX + length - length / 2 + i][startY + length - length / 2 + j];
                matrix[startX + length - length / 2 + i][startY + length - length / 2 + j] = matrix[startX + i][startY + length - length / 2 + j];
                matrix[startX + i][startY + length - length / 2 + j] = temp;
            }
        }

        if(length % 2 != 0){
            for(int i = 0; i < length / 2; i++){
                int temp = matrix[startX + i][startY + length / 2];
                matrix[startX + i][startY + length / 2] = matrix[startX + length / 2][startY + i];
                matrix[startX + length / 2][startY + i] = matrix[startX + length - i - 1][startY + length / 2];
                matrix[startX + length - i - 1][startY + length / 2] = matrix[startX + length / 2][startY + length - i - 1];
                matrix[startX + length / 2][startY + length - i - 1] = temp;
            }
        }

        if(length > 3){
            rotate(matrix, startX, startY, length / 2);
            rotate(matrix, startX + length - length / 2, startY, length / 2);
            rotate(matrix, startX, startY + length - length / 2, length / 2);
            rotate(matrix, startX + length - length / 2, startY + length - length / 2, length / 2);
        }
    }
}
```
### Best Java Solution
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n / 2; ++i) {
            for (int j = i; j < n - 1 - i; ++j) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n - 1 - j][i];
                matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
                matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
                matrix[j][n - 1 - i] = tmp;
            }
        }
    }
}
```