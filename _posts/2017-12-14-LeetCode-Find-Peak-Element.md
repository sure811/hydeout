---
layout: post
title: LeetCode - Find Peak Element
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

A peak element is an element that is greater than its neighbors.

Given an input array where num`[i]` ≠ num`[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num`[-1]` = num`[n]` = -∞.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.
<!--more-->

**Note:**

Your solution should be in logarithmic complexity.

### Java Solution
```java
    public int findPeakElement(int[] nums) {
        if(nums.length == 0)
            return -1;
        if(nums.length == 1)
            return 0;
        int start = 0;
        int end = nums.length - 1;
        int mid = 0;
        while(start <= end){
            mid = (start + end) / 2;
            if((mid == 0 || nums[mid] > nums[mid - 1])
                    && (mid == nums.length - 1 || nums[mid] > nums[mid + 1]))
                return mid;
            if((mid == 0 || nums[mid] > nums[mid - 1])
                    && (mid != nums.length - 1 || nums[mid] < nums[mid + 1]))
                start = mid + 1;
            else
                end = mid - 1;
            System.out.println(start + ":" + end);
        }
        return mid;
    }
```
