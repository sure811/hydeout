---
layout: post
title: LeetCode - Permutation in String
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Two Pointers
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.
<!--more-->

**Example 1:**
```
Input:s1 = "ab" s2 = "eidbaooo"
Output:True
Explanation: s2 contains one permutation of s1 ("ba").
```
**Example 2:**
```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```
**Note:**
1. The input strings only contain lower case letters.
2. The length of both given strings is in range [1, 10,000].
### Java Solution
```java
public boolean checkInclusion(String s1, String s2) {
    int n1 = s1.length(), n2 = s2.length(), cnt = n1, left = 0;
    int[] m = new int[128];
    for (char c : s1.toCharArray())
        m[c]++;
    for (int right = 0; right < n2; right++) {
        if (m[s2.charAt(right)]-- > 0)
            --cnt;
        while (cnt == 0) {
            if (right - left + 1 == n1) return true;
            if (++m[s2.charAt(left++)] > 0) ++cnt;
        }
    }
    return false;
}
```