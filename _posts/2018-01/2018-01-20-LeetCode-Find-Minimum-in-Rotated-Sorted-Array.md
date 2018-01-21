---
layout: post
title: LeetCode - Find Minimum in Rotated Sorted Array
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.
<!--more-->
### Java Solution
```java
public int findMin(int[] nums) {
    int left = 0;
    int right = nums.length - 1;
    while(left < right) {
        int mid = (left + right) / 2;
        System.out.println(nums[left] + "|" + nums[mid] + "|" + nums[right]);
        if(nums[left] < nums[right])
            return nums[left];
        if(nums[mid] > nums[right])
            left = mid + 1;
        else
            right = mid;
    }
    System.out.println(left + " :" + right);
    return nums[left];
}
```