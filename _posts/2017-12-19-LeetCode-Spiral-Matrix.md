---
layout: post
title: LeetCode - Spiral Matrix
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.
<!--more-->

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```
You should return `[1,2,3,6,9,8,7,4,5]`.
### Java Solution
```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new LinkedList<>();
    if(matrix.length == 0)
        return result;
    int level = 0;
    int m = matrix.length;
    int n = matrix[0].length;
    int i = 0;
    int j = 0;
    int direction = 0;
    while(result.size() < m * n){
        result.add(matrix[i][j]);
        if(direction == 0){
            if(j + level == n - 1){
                i++;
                direction = 1;
            }else
                j++;
        }else if(direction == 1){
            if(i + level == m - 1){
                j--;
                direction = 2;
            }else
                i++;
        }else if(direction == 2){
            if(j - level == 0){
                i--;
                direction = 3;
            }else
                j--;
        }else if(direction == 3){
            if(i - level == 1){
                j++;
                direction = 0;
                level++;
            }else
                i--;
        }
    }
    return result;
}
```