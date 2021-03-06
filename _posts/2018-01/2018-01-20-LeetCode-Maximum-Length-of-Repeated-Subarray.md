---
layout: post
title: LeetCode - Maximum Length of Repeated Subarray
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

**Example 1:**
```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation:
The repeated subarray with maximum length is [3, 2, 1].
```
**Note:**
1. 1 <= len(A), len(B) <= 1000
2. 0 <= `A[i]`, `B[i]` < 100
### My Java Solution
```java
public int findLength(int[] A, int[] B) {
    int[][] dp = new int[A.length + 1][B.length + 1];
    int max = 0;
    for(int i = A.length - 1; i >= 0; i--){
        for(int j = B.length - 1; j >= 0; j--){
            if(A[i] == B[j]){
                dp[i][j] = dp[i + 1][j + 1] + 1;
                if(dp[i][j] > max)
                    max = dp[i][j];
            }else
                dp[i][j] = 0;
        }
    }
    return max;
}
```