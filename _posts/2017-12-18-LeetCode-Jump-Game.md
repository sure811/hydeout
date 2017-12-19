---
layout: post
title: LeetCode - Jump Game
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Greedy
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.
<!--more-->

For example:
A = `[2,3,1,1,4]`, return true.

A = `[3,2,1,0,4]`, return false.

### Java Solution
```java
public boolean canJump(int[] nums) {
    int maxIdx = 0;
    for (int i = 0; i < nums.length; ++i) {
        if (i > maxIdx || maxIdx >= nums.length - 1) break;
        maxIdx = Math.max(maxIdx, i + nums[i]);
    }
    return maxIdx >= nums.length - 1;
}
```
