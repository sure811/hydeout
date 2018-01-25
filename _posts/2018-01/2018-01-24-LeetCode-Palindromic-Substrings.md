---
layout: post
title: LeetCode - Palindromic Substrings
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.
<!--more-->

Example 1:
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
Example 2:
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```
**Note:**
1. The input string length won't exceed 1000.
### My Java Solution
```java
public int countSubstrings(String s) {
    boolean[][] pal = new boolean[s.length()][s.length()];
    int[][] dp = new int[s.length()][s.length()];
    for(int length = 0; length < s.length(); length++){
        for(int start = 0; start + length < s.length(); start++){
            if(length == 0){
                dp[length][start] = 1;
                pal[length][start] = true;
            }else if(length == 1){
                dp[length][start] = s.charAt(start) == s.charAt(start + 1) ? 3 : 2;
                pal[length][start] = s.charAt(start) == s.charAt(start + 1) ? true : false;
            }else {
                dp[length][start] = dp[length - 1][start] + dp[length - 1][start + 1]
                    - dp[length - 2][start + 1];
                pal[length][start] = s.charAt(start) == s.charAt(start + length) && pal[length - 2][start + 1] ? true : false;
                dp[length][start] += pal[length][start] ? 1 : 0;
            }
        }
    }
    return dp[s.length() - 1][0];
}
```
### Best Java Solution
```java
public int countSubstrings(String s) {
    int n = s.length(), res = 0;
    boolean[][] dp = new boolean[n][n];
    for (int i = n - 1; i >= 0; --i) {
        for (int j = i; j < n; ++j) {
            dp[i][j] = (s.charAt(i) == s.charAt(j)) && (j - i <= 2 || dp[i + 1][j - 1]);
            if (dp[i][j]) ++res;
        }
    }
    return res;
}
```