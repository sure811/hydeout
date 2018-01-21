---
layout: post
title: LeetCode - Subarray Sum Equals K
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.
<!--more-->

**Example 1:**
```
Input:nums = [1,1,1], k = 2
Output: 2
```
**Note:**
1. The length of the array is in range `[1, 20,000]`.
2. The range of numbers in the array is `[-1000, 1000]` and the range of the integer k is `[-1e7, 1e7]`.
### My Java Solution
```java
public int subarraySum(int[] nums, int k) {
    int[] sum = new int[nums.length + 1];
    for(int i = 1; i <= nums.length; i++)
        sum[i] = sum[i - 1] + nums[i - 1];
    int count = 0;
    for(int i = 0; i <= nums.length; i++){
        for(int j = i + 1; j <= nums.length; j++){
            if(sum[j] - sum[i] == k) count++;
        }
    }
    return count;
}
```
### Best Java Solution
```java
public int subarraySum(int[] nums, int k) {
    int sum = 0, result = 0;
    Map<Integer, Integer> preSum = new HashMap<>();
    preSum.put(0, 1);

    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (preSum.containsKey(sum - k)) {
            result += preSum.get(sum - k);
        }
        preSum.put(sum, preSum.getOrDefault(sum, 0) + 1);
    }

    return result;
}
```