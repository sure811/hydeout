---
layout: post
title: LeetCode - Maximal Square
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.
<!--more-->

For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
Return 4.
### Java Solution
```java
public int maximalSquare(char[][] matrix) {
    if(matrix.length == 0) return 0;
    int[][] dp = new int[matrix.length + 1][matrix[0].length + 1];
    int max = 0;
    for(int i = 1; i <= matrix.length; i++){
        for(int j = 1; j <= matrix[i - 1].length; j++){
            if(matrix[i - 1][j - 1] == '1'){
                if(dp[i - 1][j - 1] > 0){
                    int k = 1;
                    for(; k <= dp[i - 1][j - 1]; k++)
                        if(matrix[i - k - 1][j - 1] == '0' || matrix[i - 1][j - k - 1] == '0'){
                            break;
                        }
                    dp[i][j] = k;
                }else
                    dp[i][j] = 1;
                if(dp[i][j] > max)
                    max = dp[i][j];
            }
        }
    }
    return max * max;
}
```