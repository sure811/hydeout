---
layout: post
title: LeetCode - Longest Word in Dictionary
categories:
    - LeetCode
tags:
    - LeetCode
    - Easy
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.

If there is no answer, return the empty string.

**Example 1:**
```
Input:
words = ["w","wo","wor","worl", "world"]
Output: "world"
Explanation:
The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
```
**Example 2:**
```
Input:
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]
Output: "apple"
Explanation:
Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
```
**Note:**

1. All the strings in the input will only contain lowercase letters.
2. The length of words will be in the range `[1, 1000]`.
3. The length of `words[i]` will be in the range `[1, 30]`.

### Java Solution
```java
public String longestWord(String[] words) {
    Set<String> set = new HashSet<>();
    for(String word : words)
        set.add(word);
    String result = null;
    for(String word : words){
        String sub = "";
        boolean match = true;
        for(char c : word.toCharArray()){
            sub += c;
            if(!set.contains(sub)){
                match = false;
                break;
            }
        }
        if(match && (result == null || (word.length() > result.length()) || (word.length() == result.length() && word.compareTo(result) < 0)))
            result = word;
    }
    return result;
}
```