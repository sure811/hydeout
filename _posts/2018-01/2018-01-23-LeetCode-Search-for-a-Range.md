---
layout: post
title: LeetCode - Search for a Range
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return `[-1, -1]`.
<!--more-->

For example,
Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.
### My Java Solution
```java
public int[] searchRange(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    while(left <= right){
        int mid = (left + right) / 2;
        if(nums[mid] == target){
            int _right = mid - 1;
            while(left <= _right){
                int _mid = (left + _right) / 2;
                if(nums[_mid] == target){
                    _right = _mid - 1;
                }else{
                    left = _mid + 1;
                }
            }
            int min = left;
            left = mid + 1;
            while(left <= right){
                int _mid = (left + right) / 2;
                if(nums[_mid] == target){
                    left = _mid + 1;
                }else{
                    right = _mid - 1;
                }
            }
            return new int[]{min, right};
        }
        if(nums[mid] > target){
            right = mid - 1;
        }else{
            left = mid + 1;
        }
    }
    return new int[]{-1, -1};
}
```