---
layout: post
title: LeetCode - Minimum Moves to Equal Array Elements II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.
<!--more-->
**Example:**
```
Input:
[1,2,3]

Output:
2

Explanation:
Only two moves are needed (remember each move increments or decrements one element):

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```
### Java Solution
```java
public int minMoves2(int[] nums) {
    double min = Integer.MAX_VALUE;
    Arrays.sort(nums);
    for(int i = 0; i < nums.length; i++){
        if(i > 0 && nums[i] == nums[i - 1]) continue;
        double sum = 0;
        for(int num : nums) sum += Math.abs((double)num - nums[i]);
        if(sum < min) min = sum;
    }
    return (int)min;
}
```