---
layout: post
title: LeetCode - Longest Palindromic Substring
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
<!--more-->

Example:
```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
```

Example:
```
Input: "cbbd"

Output: "bb"
```
### Java Solution
```java
public String longestPalindrome(String s) {
    boolean[][] dp = new boolean[s.length()][s.length()];
    int left = 0, right = 0, len = 0;
    for (int i = 0; i < s.length(); ++i) {
        for (int j = 0; j < i; ++j) {
            dp[j][i] = (s.charAt(i) == s.charAt(j) && (i - j < 2 || dp[j + 1][i - 1]));
            if (dp[j][i] && len < i - j + 1) {
                len = i - j + 1;
                left = j;
                right = i;
            }
        }
        dp[i][i] = true;
    }
    return s.substring(left, right + 1);
}
```