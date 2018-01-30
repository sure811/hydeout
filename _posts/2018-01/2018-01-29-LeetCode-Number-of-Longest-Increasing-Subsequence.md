---
layout: post
title: LeetCode - Number of Longest Increasing Subsequence
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an unsorted array of integers, find the number of longest increasing subsequence.
<!--more-->
**Example 1:**
```
Input: [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```
**Example 2:**
```
Input: [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```
**Note: **Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.
### Java Solution
```java
public int findNumberOfLIS(int[] nums) {
    int[][] dp = new int[nums.length][2];
    int max = 0;
    int maxCount = 0;
    for(int i = 0; i < nums.length; i++){
        int length = 0;
        int count = 1;
        for(int j = 0; j < i; j++){
            if(nums[j] < nums[i]){
                if(dp[j][0] > length){
                    length = dp[j][0];
                    count = dp[j][1];
                } else if(dp[j][0] == length){
                    count += dp[j][1];
                }
            }
        }
        dp[i][0] = length + 1;
        dp[i][1] = count;
        if(length > max){
            max = length;
            maxCount = count;
        } else if (length == max){
            maxCount += count;
        }
    }
    return maxCount;
}
```