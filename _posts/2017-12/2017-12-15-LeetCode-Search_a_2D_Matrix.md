---
layout: post
title: LeetCode - Search a 2D Matrix
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Combination
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.
<!--more-->

**Note:**
* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.
For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]` and target 8,
A solution set is:
```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
### Java Solution
```java
public boolean searchMatrix(int[][] matrix, int target) {
    if(matrix.length == 0 || matrix[0].length == 0 || target < matrix[0][0] || target > matrix[matrix.length - 1][matrix[0].length - 1])
        return false;
    int iLeft = 0;
    int iRight = matrix.length - 1;
    while(iLeft <= iRight){
        int mid = (iLeft + iRight) / 2;
        if(matrix[mid][0] == target)
            return true;
        if(matrix[mid][0] > target)
            iRight = mid - 1;
        else
            iLeft = mid + 1;
    }
    System.out.println(iLeft + ":" + iRight);
    int i = iRight;
    int jLeft = 0;
    int jRight = matrix[0].length - 1;
    while(jLeft <= jRight){
        int mid = (jLeft + jRight) / 2;
        System.out.println(iLeft + ":" + iRight);
        if(matrix[i][mid] == target)
            return true;
        if(matrix[i][mid] > target)
            jRight = mid - 1;
        else
            jLeft = mid + 1;
    }
    return false;
}
```
