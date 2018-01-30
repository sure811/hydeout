---
layout: post
title: LeetCode - Range Sum Query 2D - Immutable
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

Range Sum Query 2D
The above rectangle (with the red border) is defined by (row1, col1) = (2, 1) and (row2, col2) = (4, 3), which contains sum = 8.
<!--more-->
```
Example:
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
**Note:**
1. You may assume that the matrix does not change.
2. There are many calls to sumRegion function.
3. You may assume that row1 ≤ row2 and col1 ≤ col2.
### Java Solution
```java
class NumMatrix {
    private int[][] sum;
    public NumMatrix(int[][] matrix) {
        if(matrix.length == 0)
            return;
        sum = new int[matrix.length][matrix[0].length];
        for(int i = 0; i < matrix.length; i++){
            for(int j = 0; j < matrix[0].length; j++){
                if (i == 0 && j == 0){
                    sum[i][j] = matrix[0][0];
                } else {
                    if (i != 0 && j != 0) {
                        sum[i][j] = matrix[i][j] + sum[i - 1][j] + sum[i][j - 1] - sum[i - 1][j - 1];
                    }
                    else if (i != 0) {
                        sum[i][j] = matrix[i][j] + sum[i - 1][j];
                    }
                    else if (j != 0) {
                        sum[i][j] = matrix[i][j] + sum[i][j - 1];
                    }
                }
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return sum[row2][col2] - (row1 > 0 ? sum[row1 - 1][col2] : 0) - ( col1 > 0 ? sum[row2][col1 - 1] : 0 ) + ( row1 > 0 && col1 > 0 ? sum[row1 - 1][col1 - 1] : 0);
    }
}
```