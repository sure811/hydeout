---
layout: post
title: LeetCode - Reorganize String
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string S, check if the letters can be rearranged so that two characters that are adjacent to each other are not the same.

If possible, output any possible result.  If not possible, return the empty string.
<!--more-->
**Example 1:**
```
Input: S = "aab"
Output: "aba"
```
**Example 2:**
```
Input: S = "aaab"
Output: ""
```
**Note:**

* S will consist of lowercase letters and have length in range `[1, 500]`.
### Java Solution
```java
public String reorganizeString(String S) {
    Map<Character, Integer> map = new HashMap<>();

    for(char c : S.toCharArray()){
        map.putIfAbsent(c, 0);
        map.put(c, map.get(c) + 1);
    }

    map = map.entrySet().stream().sorted((e1, e2) ->
    e2.getValue() - e1.getValue())
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue,
            (e1, e2) -> e1, LinkedHashMap::new));
    StringBuilder sb = new StringBuilder();
    int index = 1;
    for(Map.Entry<Character, Integer> entry : map.entrySet()){
        int count = entry.getValue();
        if(sb.length() == 0){
            if(count * 2 > (S.length() + 1))
                return "";
            while(--count >= 0){
                sb.append(entry.getKey());
            }
        }else{
            while(--count >= 0){
                sb.insert(index, entry.getKey());
                index = (index + 2) % sb.length();
            }
        }
    }
    return sb.toString();
}
```