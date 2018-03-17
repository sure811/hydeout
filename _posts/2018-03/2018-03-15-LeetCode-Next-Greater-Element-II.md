---
layout: post
title: LeetCode - Next Greater Element II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.
<!--more-->

**Example 1:**
```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2;
The number 2 can't find next greater number;
The second 1's next greater number needs to search circularly, which is also 2.
```
**Note:** The length of given array won't exceed 10000.
### Java Solution
```java
public int[] nextGreaterElements(int[] nums) {
    int[] results = new int[nums.length];
    for(int i = 0; i < results.length; i++){
        int j = (i + 1) % nums.length;
        while(j != i && nums[i] >= nums[j]) j = (j + 1) % nums.length;
        if(j == i)
            results[i] = -1;
        else
            results[i] = nums[j];
    }
    return results;
}
```