---
layout: post
title: LeetCode - Permutation in String
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
2. The length of both given strings is in range `[1, 10,000]`.
### Java Solution
```java
public boolean checkInclusion(String s1, String s2) {
    int[] contains = new int[26];
    for(char c : s1.toCharArray())
        contains[c - 'a']++;

    for(int i = 0; i < s2.length(); i++){
        int[] temp = new int[26];
        int j = 0;
        for(; j < s1.length(); j++){
            temp[s2.charAt((i + j) % s2.length()) - 'a']++;
            if(temp[s2.charAt((i + j) % s2.length()) - 'a'] > contains[s2.charAt((i + j) % s2.length()) - 'a'])
                break;
        }
        if(j == s1.length()) return true;
    }
    return false;
}
```