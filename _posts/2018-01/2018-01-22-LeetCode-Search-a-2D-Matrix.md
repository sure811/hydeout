---
layout: post
title: LeetCode - Search a 2D Matrix
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.
<!--more-->
For example,

Consider the following matrix:
```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```
Given target = 3, return true.
### My Java Solution
```java
public boolean searchMatrix(int[][] matrix, int target) {
    if(matrix.length == 0 || matrix[0].length == 0) return false;
    int level = 0;
    while(level < matrix.length){
        if(target < matrix[level][0]) return false;
        int left = 0;
        int right = matrix[0].length - 1;
        while(left <= right){
            int mid = (left + right) / 2;
            if(matrix[level][mid] == target) return true;
            if(matrix[level][mid] > target)
                right = mid - 1;
            else
                left = mid + 1;
        }
        level++;
    }
    return false;
}
```
### Best Java Solution
```java
public boolean searchMatrix(int[][] matrix, int target) {
    int i = 0, j = matrix[0].length - 1;
    while (i < matrix.length && j >= 0) {
            if (matrix[i][j] == target) {
                return true;
            } else if (matrix[i][j] > target) {
                j--;
            } else {
                i++;
            }
        }

    return false;
}
```