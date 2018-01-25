---
layout: post
title: LeetCode - Integer Break
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.
<!--more-->

For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

Note: You may assume that n is not less than 2 and not larger than 58.
### Java Solution
```java
public int integerBreak(int n) {
    int[] dp = new int[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    for(int i = 2; i <= n; i++){
        for(int j = 1; j < i; j++)
            dp[i] = Math.max(Math.max(i - j, dp[i - j]) * j, dp[i]);
    }
    return dp[n];
}
```