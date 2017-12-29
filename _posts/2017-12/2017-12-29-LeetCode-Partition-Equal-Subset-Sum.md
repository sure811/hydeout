---
layout: post
title: LeetCode - Partition Equal Subset Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.
<!--more-->

**Note:**
1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.
**Example 1:**
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```
**Example 2:**
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```
### Java Solution
```java
public boolean canPartition(int[] nums) {
    int sum = 0;
    for(int num : nums)
        sum += num;
    if (sum % 2 == 1) return false;
    sum = sum / 2;
    boolean[] dp = new boolean[sum + 1];
    dp[0] = true;
    for (int i = 0; i < nums.length; ++i) {
        for (int j = sum; j >= nums[i]; --j) {
            dp[j] = dp[j] || dp[j - nums[i]];
        }
    }
    return dp[sum];
}
```