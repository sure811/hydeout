---
layout: post
title: LeetCode -
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.
<!--more-->

For example,
Given the following matrix:

[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
### My Java Solution
```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new LinkedList<>();
    if(matrix.length == 0 || matrix[0].length == 0) return result;
    int n = matrix.length,m = matrix[0].length, count = 1, i = 0, j = 0, direct = 0, leveli = n, levelj = m;
    while (count <= n * m) {
        result.add(matrix[i][j]);
        if(direct == 0){
            j++;
            if(j == levelj){
                j--;
                i++;
                direct = 1;
            }
        } else if(direct == 1){
            i++;
            if(i == leveli){
                i--;
                j--;
                direct = 2;
            }
        } else if(direct == 2){
            j--;
            if(j == m - levelj - 1){
                i--;
                j++;
                direct = 3;
            }
        } else {
            i--;
            if(i == n - leveli){
                i++;
                j++;
                direct = 0;
                leveli--;
                levelj--;
            }
        }
        count++;
    }
    return result;
}
```