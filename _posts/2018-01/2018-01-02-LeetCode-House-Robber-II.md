---
layout: post
title: LeetCode - House Robber II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Note: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
<!--more-->
### Java Solution
```java
public int rob(int[] nums) {
    if (nums.length <= 1) return nums.length == 0 ? 0 : nums[0];
    return Math.max(rob(nums, 0, nums.length - 1), rob(nums, 1, nums.length));
}

private int rob(int[] nums, int left, int right) {
    if (right - left <= 1) return nums[left];
    int[] dp = new int[right];
    dp[left] = nums[left];
    dp[left + 1] = Math.max(nums[left], nums[left + 1]);
    for (int i = left + 2; i < right; ++i) {
        dp[i] = Math.max(nums[i] + dp[i - 2], dp[i - 1]);
    }
    return dp[right - 1];
}
```