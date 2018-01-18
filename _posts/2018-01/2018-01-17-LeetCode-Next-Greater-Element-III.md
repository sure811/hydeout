---
layout: post
title: LeetCode - Next Greater Element III
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a positive 32-bit integer n, you need to find the smallest 32-bit integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive 32-bit integer exists, you need to return -1.
<!--more-->

Example 1:
```
Input: 12
Output: 21
```
Example 2:
```
Input: 21
Output: -1
```
### Java Solution
```java
public int nextGreaterElement(int n) {
    if(n <= 11) return -1;
    char[] nums = Integer.toString(n).toCharArray();
    int start = nums.length - 1;
    while(start >= 1 && nums[start] <= nums[start - 1]) start--;
    if(start == 0) return -1;
    int end = nums.length - 1;
    while(end >= start && nums[end] <= nums[start - 1]) end--;
    char temp = nums[start - 1];
    nums[start - 1] = nums[end];
    nums[end] = temp;
    end = nums.length - 1;
    while(start < end){
        temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
    double result = Double.parseDouble(new String(nums));
    if(result > Integer.MAX_VALUE) return -1;
    return (int)result;
}
```