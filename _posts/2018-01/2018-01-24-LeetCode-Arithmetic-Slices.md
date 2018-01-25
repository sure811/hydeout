---
layout: post
title: LeetCode - Arithmetic Slices
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.
<!--more-->

For example, these are arithmetic sequence:
```
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```
The following sequence is not arithmetic.
```
1, 1, 2, 5, 7
```
A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.

A slice (P, Q) of array A is called arithmetic if the sequence:
`A[P], A[p + 1], ..., A[Q - 1], A[Q]` is arithmetic. In particular, this means that P + 1 < Q.

The function should return the number of arithmetic slices in the array A.


**Example:**
```
A = [1, 2, 3, 4]

return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.
```
### Java Solution
```java
public int numberOfArithmeticSlices(int[] A) {
    boolean[][] dp = new boolean[A.length][A.length];
    int res = 0;
    for(int length = 2; length < A.length; length++){
        for(int start = 0; start + length < A.length; start++){
            if(length == 2){
                if(A[start + 1] - A[start] == A[start + 2] - A[start + 1]){
                    dp[start][length] = true;
                    res++;
                }
                else
                    dp[start][length] = false;
            }else{
                if(A[start + length] - A[start + length - 1] == A[start + length - 1] - A[start + length - 2] && dp[start][length - 1]){
                    dp[start][length] = true;
                    res++;
                }
                else
                    dp[start][length] = false;
            }
        }
    }
    return res;
}
```