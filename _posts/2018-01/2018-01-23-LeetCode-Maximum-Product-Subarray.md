---
layout: post
title: LeetCode - Maximum Product Subarray
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = 6.
### Java Solution
```java
public int maxProduct(int[] nums) {
    if (nums == null || nums.length == 0) {
        return 0;
    }
    int max = nums[0], min = nums[0], result = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int temp = max;
        max = Math.max(Math.max(max * nums[i], min * nums[i]), nums[i]);
        min = Math.min(Math.min(temp * nums[i], min * nums[i]), nums[i]);
        if (max > result) {
            result = max;
        }
    }
    return result;
    }
```