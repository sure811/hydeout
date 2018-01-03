---
layout: post
title: LeetCode - Partition to K Equal Sum Subsets
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into k non-empty subsets whose sums are all equal.
<!--more-->

**Example 1:**
```
Input: nums = [4, 3, 2, 3, 5, 2, 1], k = 4
Output: True
Explanation: It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```
**Note:**

* 1 <= k <= len(nums) <= 16.
* 0 < `nums[i]` < 10000.
### Java Solution
```java
public boolean canPartitionKSubsets(int[] nums, int k) {
    int sum = 0;
    for(int num : nums){
        sum += num;
    }

    if(sum % k != 0)
        return false;
    int target = sum / k;
    int[] v = new int[k];
    Arrays.sort(nums);

    return helper(nums, target, v, nums.length - 1);
}

private boolean helper(int[] nums, int target, int[] v, int idx) {
    if (idx == -1) {
        for (int t : v) {
            if (t != target) return false;
        }
        return true;
    }
    int num = nums[idx];
    for (int i = 0; i < v.length; ++i) {
        if (v[i] + num > target) continue;
        v[i] += num;
        if (helper(nums, target, v, idx - 1)) return true;
        v[i] -= num;
    }
    return false;
}
```