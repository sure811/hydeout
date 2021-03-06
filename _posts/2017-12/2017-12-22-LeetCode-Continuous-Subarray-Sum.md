---
layout: post
title: LeetCode - Continuous Subarray Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a list of non-negative numbers and a target integer k, write a function to check if the array has a continuous subarray of size at least 2 that sums up to the multiple of k, that is, sums up to n*k where n is also an integer.
<!--more-->

**Example 1:**
```
Input: [23, 2, 4, 6, 7],  k=6
Output: True
Explanation: Because [2, 4] is a continuous subarray of size 2 and sums up to 6.
```
**Example 2:**
```
Input: [23, 2, 6, 4, 7],  k=6
Output: True
Explanation: Because [23, 2, 6, 4, 7] is an continuous subarray of size 5 and sums up to 42.
```
**Note:**
The length of the array won't exceed 10,000.
You may assume the sum of all the numbers is in the range of a signed 32-bit integer.

### Java Solution
```java
public boolean checkSubarraySum(int[] nums, int k) {
    if(nums.length == 0)
        return false;
    int[] sum = new int[nums.length];
    sum[0] = nums[0];
    for(int i = 1; i < nums.length; i++)
        sum[i] = nums[i] + sum[i - 1];
    for(int i = 1; i < nums.length; i++){
        if((k == 0 && sum[i] == 0) || (k != 0 && sum[i] % k == 0))
            return true;
        for(int j = 0; j < i - 1; j++){
            if((k == 0 && (sum[i] - sum[j]) == 0) || (k != 0 && (sum[i] - sum[j]) % k == 0))
                return true;
        }
    }
    return false;
}
```