---
layout: post
title: LeetCode - Majority Element II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Moore Voting
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.
<!--more-->

### Java Solution
```java
public List<Integer> majorityElement(int[] nums) {
    List<Integer> result = new LinkedList<>();
    int m = 0, n = 0, cm = 0, cn = 0;
    for(int num : nums){
        if (num == m) ++cm;
        else if (num ==n) ++cn;
        else if (cm == 0) {
            m = num;
            cm = 1;
        }
        else if (cn == 0) {
            n = num;
            cn = 1;
        }
        else{
            --cm;
            --cn;
        }
    }
    cm = 0;
    cn = 0;
    for (int num : nums) {
        if (num == m) ++cm;
        else if (num == n) ++cn;
    }
    if (cm > nums.length / 3) result.add(m);
    if (cn > nums.length / 3) result.add(n);
    return result;
}
```
