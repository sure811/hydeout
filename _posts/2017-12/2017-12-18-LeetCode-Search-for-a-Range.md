---
layout: post
title: LeetCode - Search for a Range
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.
<!--more-->

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.

For example,
Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.

### Java Solution
```java
public int[] searchRange(int[] nums, int target) {
    if(nums.length == 0)
        return new int[]{-1, -1};
    int left = 0;
    int right = nums.length - 1;
    while(left <= right){
        int mid = (left + right) / 2;
        if(nums[mid] == target){
            int start = mid;
            int end = mid;
            while(--start >= 0 && nums[start] == target);
            while(++end < nums.length && nums[end] == target);
            return new int[]{start + 1, end - 1};
        }else if(nums[mid] > target){
            right = mid - 1;
        }else{
            left = mid + 1;
        }
    }
    return new int[]{-1, -1};
}
```