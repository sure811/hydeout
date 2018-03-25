---
layout: post
title: LeetCode - Maximum Product of Word Lengths
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string array words, find the maximum value of `length(word[i]) * length(word[j])` where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.
<!--more-->

**Example 1:**
Given `["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]`
Return 16
The two words can be "abcw", "xtfn".

**Example 2:**
Given `["a", "ab", "abc", "d", "cd", "bcd", "abcd"]`
Return 4
The two words can be "ab", "cd".

**Example 3:**
Given `["a", "aa", "aaa", "aaaa"]`
Return 0
No such pair of words.
### Java Solution
```java
public int maxProduct(String[] words) {
    int[] masks = new int[words.length];
    int result = 0;
    for(int i = 0; i < words.length; i++){
        int mask = 0;
        for(char c : words[i].toCharArray())
            mask = mask | (1 << (int)(c - 'a'));
        masks[i] = mask;
        for(int j = 0; j < i; j++)
            if((mask & masks[j]) == 0)
                result = Math.max(result, words[i].length() * words[j].length());
    }

    return result;
}
```