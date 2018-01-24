---
layout: post
title: LeetCode - 3Sum Closest
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
```
    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
### Java Solution
```java
public int threeSumClosest(int[] nums, int target) {
    int closest = nums[0] + nums[1] + nums[2];
    int diff = Math.abs(closest - target);
    Arrays.sort(nums);
    for (int i = 0; i < nums.length - 2; ++i) {
        int left = i + 1, right = nums.length - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            int newDiff = Math.abs(sum - target);
            if (diff > newDiff) {
                diff = newDiff;
                closest = sum;
            }
            if (sum < target) ++left;
            else --right;
        }
    }
    return closest;
}
```