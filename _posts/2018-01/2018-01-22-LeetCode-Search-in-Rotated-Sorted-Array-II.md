---
layout: post
title: LeetCode - Search in Rotated Sorted Array II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
<!--more-->

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Write a function to determine if a given target is in the array.

The array may contain duplicates.
### Java Solution
```java
public boolean search(int[] nums, int target) {
    int low = 0;
    int high = nums.length - 1;
    while(low <= high){
        int mid = (low + high) / 2;
        if(nums[mid] == target) return true;
        if(nums[mid] == nums[low] && nums[mid] == nums[high]){
            high--;
        }else if((nums[mid] < nums[high] && target > nums[mid] && target <= nums[high])
           ||(nums[mid] > nums[high] && (target > nums[mid] || target < nums[low]))
           ){
            while(mid < nums.length - 1 && nums[mid + 1] == nums[mid]) mid++;
            low = mid + 1;
        }else{
            while(mid > 0 && nums[mid - 1] == nums[mid]) mid--;
            high = mid - 1;
        }
    }
    return false;
}
```