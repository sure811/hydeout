---
layout: post
title: LeetCode - Word Break
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.
<!--more-->
For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".
### Java Solution
```java
public boolean wordBreak(String s, List<String> wordDict) {
    int len = s.length();
    boolean[] res = new boolean[len + 1];
    res[0] = true;
    for (int i = 0; i < len + 1; ++i) {
        for (int j = 0; j < i; ++j) {
            if (res[j] && wordDict.contains(s.substring(j, i))) {
                res[i] = true;
                break;
            }
        }
    }
    return res[len];
}
```