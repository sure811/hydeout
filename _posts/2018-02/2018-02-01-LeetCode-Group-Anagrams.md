---
layout: post
title: LeetCode - Group Anagrams
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of strings, group anagrams together.
<!--more-->
For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"]`,
Return:
```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
**Note: **All inputs will be in lower-case.
### Java Solution
```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();

    for(String str : strs){
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars);
        map.putIfAbsent(key, new LinkedList<>());
        map.get(key).add(str);
    }

    return map.values().stream().collect(Collectors.toList());
}
```