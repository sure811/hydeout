---
layout: post
title: LeetCode - Longest Substring Without Repeating Characters
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string, find the length of the longest substring without repeating characters.
<!--more-->

**Examples:**

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
### Java Solution
```java
public int lengthOfLongestSubstring(String s) {
    int[] m = new int[256];
    Arrays.fill(m, -1);
    int res = 0, left = -1;
    for (int i = 0; i < s.length(); ++i) {
        left = Math.max(left, m[s.charAt(i)]);
        m[s.charAt(i)] = i;
        res = Math.max(res, i - left);
    }
    return res;
}
```