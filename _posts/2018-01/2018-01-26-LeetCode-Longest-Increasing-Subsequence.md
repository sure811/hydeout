---
layout: post
title: LeetCode - Longest Increasing Subsequence
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an unsorted array of integers, find the length of longest increasing subsequence.
<!--more-->

For example,
Given `[10, 9, 2, 5, 3, 7, 101, 18]`,
The longest increasing subsequence is `[2, 3, 7, 101]`, therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(n2) complexity.

Follow up: Could you improve it to O(n log n) time complexity?
### Java Solution
```java
public int lengthOfLIS(int[] nums) {
    List<Integer> dp = new LinkedList<>();
    for (int i = 0; i < nums.length; ++i) {
        int left = 0, right = dp.size();
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (dp.get(mid) < nums[i]) left = mid + 1;
            else right = mid;
        }
        if (right >= dp.size()) dp.add(nums[i]);
        else dp.set(right, nums[i]);
    }
    return dp.size();
}
```