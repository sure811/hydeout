---
layout: post
title: LeetCode - Kth Largest Element in an Array
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example,
Given `[3,2,1,5,6,4]` and k = 2, return 5.

**Note: **
You may assume k is always valid, 1 ≤ k ≤ array's length.
### Java Solution
```java
public int findKthLargest(int[] nums, int k) {
    if(nums.length == 0 || k < 0 || k > nums.length) return -1;
    int start = 0;
    int end = nums.length - 1;
    while(true){
        int index = partition(nums, start, end);
        if(index == k - 1) return nums[index];
        if(index > k - 1)
            end = index - 1;
        else
            start = index + 1;
    }
}

private int partition(int[] a, int lo, int hi){
    int i = lo, j = hi+1; // left and right scan indices
    int v = a[lo]; // partitioning item
    while (true)
    { // Scan right, scan left, check for scan complete, and exchange.
        while (++i < hi && a[i] > v);
        while (--j > lo && v > a[j]) if (j == lo) break;
        if (i >= j) break;
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    int temp = a[lo];
    a[lo] = a[j];
    a[j] = temp;
    return j;
}
```