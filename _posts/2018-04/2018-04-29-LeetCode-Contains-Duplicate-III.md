---
layout: post
title: LeetCode - Contains Duplicate III
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between `nums[i]` and `nums[j]` is at most t and the absolute difference between i and j is at most k.
### Java Solution
```java
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    if (nums == null || nums.length == 0 || k <= 0) {
        return false;
    }

    final TreeSet<Double> values = new TreeSet<>();
    for (int ind = 0; ind < nums.length; ind++) {

        final Double floor = values.floor((double)nums[ind] + t);
        final Double ceil = values.ceiling((double)nums[ind] - t);
        if ((floor != null && floor >= nums[ind])
                || (ceil != null && ceil <= nums[ind])) {
            return true;
        }

        values.add((double)nums[ind]);
        if (ind >= k) {
            values.remove((double)nums[ind - k]);
        }
    }

    return false;
}
```