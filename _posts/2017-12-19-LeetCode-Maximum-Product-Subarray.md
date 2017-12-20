---
layout: post
title: LeetCode - Maximum Product Subarray
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition

Find the contiguous subarray within an array (containing at least one number) which has the largest product.
<!--more-->

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = 6.

### Java Solution
```java
public int maxProduct(int[] nums) {
    int[] min = new int[nums.length];
    int[] max = new int[nums.length];
    int result = nums[0];
    min[0] = nums[0];
    max[0] = nums[0];
    for(int i = 1; i < nums.length; i++){
        max[i] = Math.max(Math.max(nums[i] * min[i - 1], nums[i] * max[i - 1]), nums[i]);
        min[i] = Math.min(Math.min(nums[i] * min[i - 1], nums[i] * max[i - 1]), nums[i]);
        if(max[i] > result)
            result = max[i];
    }
    return result;
}
```