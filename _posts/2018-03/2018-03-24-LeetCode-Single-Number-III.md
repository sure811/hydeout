---
layout: post
title: LeetCode - Single Number III
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.
<!--more-->
For example:

Given nums = `[1, 2, 1, 3, 2, 5]`, return `[3, 5]`.

**Note:**
1. The order of the result is not important. So in the above example, `[5, 3]` is also correct.
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?
### Java Solution
```java
public int[] singleNumber(int[] nums) {
    int bit = nums[0];
    for(int i = 1; i < nums.length; i++)
        bit = bit ^ nums[i];
    bit &= -bit;
    int[] result = new int[2];
    for(int num : nums){
        if ((num & bit) != 0) result[0] ^= num;
        else result[1] ^= num;
    }
    return result;
}
```