---
layout: post
title: LeetCode - Spiral Matrix II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.
<!--more-->

For example,
Given n = 3,

You should return the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```
### My Java Solution
```java
public int[][] generateMatrix(int n) {
    int[][] result = new int[n][n];
    int count = 1, i = 0, j = 0, direct = 0, level = n;
    while (count <= n * n) {
        result[i][j] = count;
        if(direct == 0){
            j++;
            if(j == level){
                j--;
                i++;
                direct = 1;
            }
        } else if(direct == 1){
            i++;
            if(i == level){
                i--;
                j--;
                direct = 2;
            }
        } else if(direct == 2){
            j--;
            if(j == n - level - 1){
                i--;
                j++;
                direct = 3;
            }
        } else {
            i--;
            if(i == n - level){
                i++;
                j++;
                direct = 0;
                level--;
            }
        }
        count++;
    }
    return result;
}
```