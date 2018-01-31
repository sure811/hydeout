---
layout: post
title: LeetCode - Delete and Earn
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array nums of integers, you can perform operations on the array.

In each operation, you pick any `nums[i]` and delete it to earn `nums[i]` points. After, you must delete every element equal to `nums[i]` - 1 or `nums[i]` + 1.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.
<!--more-->

**Example 1:**
```
Input: nums = [3, 4, 2]
Output: 6
Explanation:
Delete 4 to earn 4 points, consequently 3 is also deleted.
Then, delete 2 to earn 2 points. 6 total points are earned.
```
**Example 2:**
```
Input: nums = [2, 2, 3, 3, 3, 4]
Output: 9
Explanation:
Delete 3 to earn 3 points, deleting both 2s and the 4.
Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
9 total points are earned.
```
**Note:**

* The length of nums is at most 20000.
* Each element nums[i] is an integer in the range [1, 10000].

### Explaination
`dp[x]`: Max points you can earn if you deleted all data bigger than x

`dp[x] = max(dp[x + 1], dp[x + 2] + cnt[x] * x)`
### Java Solution
```java
public int deleteAndEarn(int[] nums) {
    int[] count = new int[10001];
    for(int n : nums){
        count[n] += n;
    }
    int[] dp = new int[10003];
    for(int i = 10000; i >= 0; i--) {
        dp[i] = Math.max(count[i] + dp[i + 2], dp[i + 1]);
    }
    return dp[0];
}
```