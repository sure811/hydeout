---
layout: post
title: LeetCode - Monotone Increasing Digits
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Greedy
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-negative integer N, find the largest number that is less than or equal to N with monotone increasing digits.

(Recall that an integer has monotone increasing digits if and only if each pair of adjacent digits x and y satisfy x <= y.)
<!--more-->
**Example 1:**
```
Input: N = 10
Output: 9
```
**Example 2:**
```
Input: N = 1234
Output: 1234
```
**Example 3:**
```
Input: N = 332
Output: 299
```
Note: N is an integer in the range `[0, 10^9]`.
### Java Solution
```java
public int monotoneIncreasingDigits(int N) {
    char[] nums = Integer.toString(N).toCharArray();
    int index = 0;
    while(index < nums.length - 1 && nums[index] <= nums[index + 1])
        index++;
    while(index > 0 && nums[index] == nums[index - 1]) index--;
    if(index == nums.length - 1) return N;
    nums[index] = (char)(((int)(nums[index] - '0') - 1) + '0');
    while(++index < nums.length) nums[index] = '9';
    return Integer.parseInt(new String(nums));
}
```