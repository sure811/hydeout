---
layout: post
title: LeetCode - Longest Substring with At Least K Repeating Characters
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Find the length of the longest substring T of a given string (consists of lowercase letters only) such that every character in T appears no less than k times.
<!--more-->

Example 1:
```
Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
```
Example 2:
```
Input:
s = "ababbc", k = 2

Output:
5

The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```
### Java Solution
```java
public int longestSubstring(String s, int k) {
    int res = 0, i = 0, n = s.length();
    while (i + k <= n) {
        int[] m = new int[26];
        int mask = 0, max_idx = i;
        for (int j = i; j < n; ++j) {
            int t = s.charAt(j) - 'a';
            ++m[t];
            if (m[t] < k) mask |= (1 << t);
            else mask &= (~(1 << t));
            if (mask == 0) {
                res = Math.max(res, j - i + 1);
                max_idx = j;
            }
        }
        i = max_idx + 1;
    }
    return res;
}
```