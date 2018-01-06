---
layout: post
title: LeetCode - Search a 2D Matrix II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.
For example,

Consider the following matrix:
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given target = 5, return true.

Given target = 20, return false.
### Java Solution
```java
public boolean searchMatrix(int[][] matrix, int target) {
    if(matrix.length == 0 || matrix[0].length == 0) return false;
    int i = 0;
    int left = 0;
    int right = matrix[0].length - 1;
    while(true){
        int mid = (left + right) / 2;
        if(matrix[i][mid] == target)
            return true;
        if(matrix[i][mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
        if(left > right){
            if(left == 0)
                return false;
            if(i == matrix.length - 1)
                return false;
            i++;
            left = 0;
            right = matrix[i].length - 1;
        }
    }
}
```