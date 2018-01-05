---
layout: post
title: LeetCode - Word Break
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.
<!--more-->

For example, given
s = "leetcode",
dict = `["leet", "code"]`.

Return true because "leetcode" can be segmented as "leet code".
### Java Solution
```java
public boolean wordBreak(String s, List<String> wordDict) {
    if(s == null || s.length() == 0)
        return true;
    boolean[] res = new boolean[s.length() + 1];
    res[0] = true;
    for(int i = 0; i < s.length(); i++)
    {
        StringBuilder str = new StringBuilder(s.substring(0, i + 1));
        for(int j=0;j<=i;j++)
        {
            if(res[j] && wordDict.contains(str.toString()))
            {
                res[i+1] = true;
                break;
            }
            str.deleteCharAt(0);
        }
    }
    return res[s.length()];
}
```