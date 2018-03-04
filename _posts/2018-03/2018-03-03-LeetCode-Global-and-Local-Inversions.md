---
layout: post
title: LeetCode - Global and Local Inversions
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
We have some permutation A of `[0, 1, ..., N - 1]`, where N is the length of A.

The number of (global) inversions is the number of i < j with 0 <= i < j < N and `A[i] > A[j]`.

The number of local inversions is the number of i with 0 <= i < N and `A[i] > A[i+1]`.

Return true if and only if the number of global inversions is equal to the number of local inversions.
<!--more-->

**Example 1:**
```
Input: A = [1,0,2]
Output: true
Explanation: There is 1 global inversion, and 1 local inversion.
```
**Example 2:**
```
Input: A = [1,2,0]
Output: false
Explanation: There are 2 global inversions, and 1 local inversion.
```
**Note:**

* A will be a permutation of `[0, 1, ..., A.length - 1]`.
* A will have length in range `[1, 5000]`.
* The time limit for this problem has been reduced.
### Java Solution
```java
public boolean isIdealPermutation(int[] A) {
    if (A.length < 2) return true;
    for (int i = 1; i < A.length; i++) {
        if (A[i-1] > A[i])
        {
            int temp = A[i];
            A[i] = A[i-1];
            A[i-1] = temp;
            if (A[i-1] != i-1 || A[i] != i) return false;
        }
    }
    return true;
}
```