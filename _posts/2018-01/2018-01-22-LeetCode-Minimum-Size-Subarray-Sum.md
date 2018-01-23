---
layout: post
title: LeetCode - Minimum Size Subarray Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
### Java Solution
```java
public int minSubArrayLen(int s, int[] nums) {
    int[] sum = new int[nums.length + 1];
    for(int i = 1; i < sum.length; i++)
        sum[i] = sum[i - 1] + nums[i - 1];
    int min = nums.length + 1;
    for(int i = 0; i < nums.length; i++){
        int needed = s + sum[i];
        int left = i + 1;
        int right = sum.length - 1;
        while(left <= right){
            int mid = (left + right) / 2;
            if(sum[mid] == needed){
                left = mid;
                break;
            }
            if(sum[mid] < needed) left = mid + 1;
            else right = mid - 1;
        }
        if(left < sum.length && left - i < min)
            min = left - i;
    }
    return min == nums.length + 1 ? 0 : min;
}
```