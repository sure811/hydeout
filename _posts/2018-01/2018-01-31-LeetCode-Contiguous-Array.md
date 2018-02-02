---
layout: post
title: LeetCode - Contiguous Array
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.
<!--more-->
**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```
**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```
**Note:** The length of the given binary array will not exceed 50,000.
### Java Solution
```java
public int findMaxLength(int[] nums) {
    int res = 0, n = nums.length, sum = 0;
    Map<Integer, Integer> m = new HashMap<>();
    m.put(0, -1);
    for (int i = 0; i < n; ++i) {
        sum += (nums[i] == 1) ? 1 : -1;
        if (m.containsKey(sum)) {
            res = Math.max(res, i - m.get(sum));
        } else {
            m.put(sum, i);
        }
    }
    return res;
}
```