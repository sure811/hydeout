---
layout: post
title: LeetCode - Increasing Triplet Subsequence
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:
Return true if there exists i, j, k
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.
Your algorithm should run in O(n) time complexity and O(1) space complexity.
<!--more-->

**Examples:**
Given `[1, 2, 3, 4, 5]`,
return true.

Given `[5, 4, 3, 2, 1]`,
return false.
### Java Solution
```java
public boolean increasingTriplet(int[] nums) {
    if(nums.length < 3) return false;
    int min = Integer.MAX_VALUE;
    int mid = Integer.MAX_VALUE;
    for(int num : nums){
        if(num < min){
            min = num;
        }else if(num > min && num < mid) {
            mid = num;
        } else if(num > mid)
            return true;
    }
    return false;
}
```