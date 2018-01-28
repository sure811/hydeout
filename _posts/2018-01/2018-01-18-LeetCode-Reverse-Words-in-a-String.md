---
layout: post
title: LeetCode - Reverse Words in a String
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an input string, reverse the string word by word.
<!--more-->

For example,
Given s = "the sky is blue",
return "blue is sky the".
### Java Solution
```java
public String reverseWords(String s) {
    String[] parts = s.trim().split("\\s+");
    String out = "";
    for (int i = parts.length - 1; i > 0; i--) {
        out += parts[i] + " ";
    }
    return out + parts[0];
}
```