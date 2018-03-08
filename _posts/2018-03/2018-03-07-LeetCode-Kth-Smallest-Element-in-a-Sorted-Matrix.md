---
layout: post
title: LeetCode - Kth Smallest Element in a Sorted Matrix
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.
<!--more-->

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example: **
```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```
**Note: **
You may assume k is always valid, 1 ≤ k ≤ n2.
### Java Solution
```java
public int kthSmallest(int[][] matrix, int k) {
    int[] indexs = new int[matrix.length];

    while(true){
        int index = -1;
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < matrix.length; i++){
            if(indexs[i] < matrix[i].length && matrix[i][indexs[i]] < min){
                min = matrix[i][indexs[i]];
                index = i;
            }
        }
        indexs[index]++;
        if(--k == 0) return min;
    }
}
```