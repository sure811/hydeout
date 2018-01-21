---
layout: post
title: LeetCode - Find Peak Element
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
A peak element is an element that is greater than its neighbors.
<!--more-->

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

**Note:**

Your solution should be in logarithmic complexity.
### My Java Solution
```java
public int findPeakElement(int[] nums) {
    if(nums.length == 1) return 0;
    for(int i = 0; i < nums.length; i++){
        if(i == 0) {
            if(nums[i] > nums[i + 1]) return i;
        }else if(i == nums.length - 1){
            if(nums[i] > nums[i - 1]) return i;
        }else if(nums[i] > nums[i + 1] && nums[i] > nums[i - 1])
            return i;
    }
    return -1;
}
```