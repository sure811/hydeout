---
layout: post
title: LeetCode - Target Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.
<!--more-->

**Example 1:**
```
Input: nums is [1, 1, 1, 1, 1], S is 3.
Output: 5
Explanation:

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```
**Note:**
1. The length of the given array is positive and will not exceed 20.
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.
### Java Solution
```java
public int findTargetSumWays(int[] nums, int S) {
    if(nums.length == 0) return 0;
    Map<Integer, Integer> result = new HashMap<>();
    result.put(0, 1);
    for(int i = 0; i < nums.length; i++){
        Map<Integer, Integer> newResult = new HashMap<>();
        for(Map.Entry<Integer, Integer> entry : result.entrySet()){
            newResult.putIfAbsent(entry.getKey() + nums[i], 0);
            newResult.putIfAbsent(entry.getKey() - nums[i], 0);
            newResult.put(entry.getKey() + nums[i], newResult.get(entry.getKey() + nums[i]) + entry.getValue());
            newResult.put(entry.getKey() - nums[i], newResult.get(entry.getKey() - nums[i]) + entry.getValue());
        }
        result = newResult;
    }
    return result.containsKey(S) ? result.get(S) : 0;
}
```