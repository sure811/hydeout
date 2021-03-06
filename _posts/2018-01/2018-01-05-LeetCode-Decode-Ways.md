---
layout: post
title: LeetCode - Decode Ways
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
A message containing letters from A-Z is being encoded to numbers using the following mapping:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.
### Java Solution
```java
public int numDecodings(String s) {
    if(s.isEmpty() || (s.length() > 1 && s.charAt(0) == '0')) return 0;
    int[] dp = new int[s.length() + 1];
    dp[0] = 1;
    for(int i = 1; i <= s.length(); i++){
        dp[i] = (s.charAt(i - 1) == '0') ? 0 : dp[i - 1];
        if (i > 1 && (s.charAt(i - 2) == '1' || (s.charAt(i - 2) == '2' && s.charAt(i - 1) <= '6'))) {
            dp[i] += dp[i - 2];
        }
    }
    return dp[s.length()];
}
```