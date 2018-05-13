---
layout: post
title: LeetCode - Diagonal Traverse
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.
<!--more-->

**Example:**
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
Explanation:
```
**Note:**
1. The total number of elements of the given matrix will not exceed 10,000.
### Java Solution
```java
public int[] findDiagonalOrder(int[][] matrix) {
    if (matrix.length == 0) return new int[0];
    int r = 0, c = 0, m = matrix.length, n = matrix[0].length, arr[] = new int[m * n];
    for (int i = 0; i < arr.length; i++) {
        arr[i] = matrix[r][c];
        if ((r + c) % 2 == 0) { // moving up
            if      (c == n - 1) { r++; }
            else if (r == 0)     { c++; }
            else            { r--; c++; }
        } else {                // moving down
            if      (r == m - 1) { c++; }
            else if (c == 0)     { r++; }
            else            { r++; c--; }
        }
    }
    return arr;
}
```