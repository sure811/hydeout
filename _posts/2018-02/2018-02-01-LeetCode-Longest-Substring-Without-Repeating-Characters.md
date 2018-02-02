---
layout: post
title: LeetCode - Longest Substring Without Repeating Characters
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
    Map<Character, Integer> map = new HashMap<>();
    int i = 0, max = 0, j = 0;
    while(j < s.length()){
        char c = s.charAt(j);
        if(!map.containsKey(c)){
            if(j - i + 1 > max)
                max = j - i + 1;
        }else{
            int end = map.get(c);
            for(int k = i; k < end; k++)
                map.remove(s.charAt(k));
            i = end + 1;
        }
        map.put(c, j);
        j++;
    }
    return max;
}
```