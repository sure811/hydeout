---
layout: post
title: LeetCode - Single Number II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one.
<!--more-->
**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
### Java Solution
```java
public int singleNumber(int[] nums) {
    int res = 0;
    for (int i = 0; i < 32; ++i) {
        int sum = 0;
        for (int j = 0; j < nums.length; ++j) {
            sum += (nums[j] >> i) & 1;
        }
        res |= (sum % 3) << i;
    }
    return res;
}
```