---
layout: post
title: LeetCode - Repeated DNA Sequences
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

For example,
```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```
### Java Solution
```java
public List<String> findRepeatedDnaSequences(String s) {
    List<String> result = new LinkedList<>();
    Map<String, Integer> map = new HashMap<>();
    for(int i = 10; i <= s.length(); i++){
        String sub = s.substring(i - 10, i);
        if(map.containsKey(sub)){
            if(map.get(sub) == 1)
                result.add(sub);
            map.put(sub, map.get(sub) + 1);
        }else
            map.put(sub, 1);
    }
    return result;
}
```