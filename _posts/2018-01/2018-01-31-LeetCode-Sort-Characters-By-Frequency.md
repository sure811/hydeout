---
layout: post
title: LeetCode - Sort Characters By Frequency
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string, sort it in decreasing order based on the frequency of characters.
<!--more-->
**Example 1:**
```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```
**Example 2:**
```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```
**Example 3:**
```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```
### Java Solution
```java
public String frequencySort(String s) {
    Map<Character, Integer> map = new HashMap<>();

    for(char c : s.toCharArray()){
        map.putIfAbsent(c, 0);
        map.put(c, map.get(c) + 1);
    }

    map = map.entrySet().stream().sorted((e1, e2) ->
    e2.getValue() - e1.getValue())
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue,
            (e1, e2) -> e1, LinkedHashMap::new));

    StringBuilder sb = new StringBuilder();
    for(Map.Entry<Character, Integer> entry : map.entrySet()){
        int times = entry.getValue();
        while(times-- > 0){
            sb.append(entry.getKey());
        }
    }
    return sb.toString();
}
```