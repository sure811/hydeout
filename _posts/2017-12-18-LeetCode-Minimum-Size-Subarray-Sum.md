---
layout: post
title: LeetCode - Minimum Size Subarray Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.
<!--more-->

For example, given the array `[2,3,1,2,4,3]` and s = 7,
the subarray `[4,3]` has the minimal length under the problem constraint.

**More practice:**

If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

### Java Solution(O(n))
```java
public int minSubArrayLen(int s, int[] nums) {
    int min = nums.length + 1;
    int sum = 0;
    int start = 0;
    for(int i = 0; i < nums.length; i++){
        sum += nums[i];
        while(sum - nums[start] >= s)
            sum -= nums[start++];
        if(sum >= s && min > i - start)
            min = i - start + 1;
    }
    return min == nums.length + 1 ? 0 : min;
}
```
### Java Solution(O(nlogn))
```java
public int minSubArrayLen(int s, int[] nums) {
    int[] sum = new int[nums.length + 1];

    for(int i = 1; i <= nums.length; i++)
        sum[i] = sum[i - 1] + nums[i - 1];

    int min = Integer.MAX_VALUE;
    for(int i = 0; i < nums.length; i++){
        int left = i + 1, right = nums.length, t = sum[i] + s;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (sum[mid] < t) left = mid + 1;
            else right = mid - 1;
        }
        if (left == nums.length + 1) break;
        min = Math.min(min, left - i);
    }
    return min == Integer.MAX_VALUE ? 0 : min;
}
```
