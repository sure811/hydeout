---
layout: post
title: LeetCode - Perfect Squares
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.
<!--more-->

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
### My Java Solution
```java
class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[1] = 1;
        return helper(n, dp);
    }

    private int helper(int n, int[] dp){
        if(dp[n] != Integer.MAX_VALUE) return dp[n];
        int sqrt = (int)Math.sqrt(n);
        if(sqrt * sqrt == n){
            dp[n] = 1;
            return 1;
        }
        for(int i = 1; i <= sqrt; i++){
            dp[n] = Math.min(helper(n - i * i, dp) + 1, dp[n]);
        }
        return dp[n];
    }
}
```