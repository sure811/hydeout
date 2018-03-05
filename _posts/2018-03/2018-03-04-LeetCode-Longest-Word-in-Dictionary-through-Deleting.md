---
layout: post
title: LeetCode - Longest Word in Dictionary through Deleting
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Two Pointers
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.
<!--more-->

**Example 1:**
```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output:
"apple"
```
**Example 2:**
```
Input:
s = "abpcplea", d = ["a","b","c"]

Output:
"a"
```
**Note:**
1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.
### Java Solution
```java
public String findLongestWord(String s, List<String> d) {
    String result = "";
    for(String word : d){
        if(word.length() < result.length())
            continue;
        int i = 0;
        int j = 0;
        for(; i < word.length() && j < s.length();){
            while(j < s.length() && word.charAt(i) != s.charAt(j)) j++;
            if(j < s.length()){
                i++;
                j++;
            }else break;
        }
        if(i == word.length() && (word.length() > result.length() || word.compareTo(result) < 0)) result = word;
    }

    return result;
}
```