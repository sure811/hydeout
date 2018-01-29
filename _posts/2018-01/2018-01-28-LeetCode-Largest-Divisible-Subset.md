---
layout: post
title: LeetCode - Largest Divisible Subset
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a set of distinct positive integers, find the largest subset such that every pair (Si, Sj) of elements in this subset satisfies: Si % Sj = 0 or Sj % Si = 0.

If there are multiple solutions, return any subset is fine.
<!--more-->

**Example 1:**
```
nums: [1,2,3]

Result: [1,2] (of course, [1,3] will also be ok)
```
**Example 2:**
```
nums: [1,2,4,8]

Result: [1,2,4,8]
```
### Java Solution
```java
public List<Integer> largestDivisibleSubset(int[] nums) {
    List<Integer> result = new LinkedList<>();
    if(nums.length == 0) return result;
    int[] dp = new int[nums.length];
    int[] parent = new int[nums.length];
    Arrays.sort(nums);
    int mx = 0, mx_idx = 0;
    for(int i = nums.length - 1; i >= 0; i--){
        for(int j = i; j < nums.length; j++){
            if(nums[j] % nums[i] == 0 && dp[i] < dp[j] + 1){
                dp[i] = dp[j] + 1;
                parent[i] = j;
                if (mx < dp[i]) {
                    mx = dp[i];
                    mx_idx = i;
                }
            }
        }
    }
    for (int i = 0; i < mx; ++i) {
        result.add(nums[mx_idx]);
        mx_idx = parent[mx_idx];
    }
    return result;
}
```