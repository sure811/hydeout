---
layout: post
title: LeetCode - Top K Frequent Words
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.
<!--more-->
**Example 1:**
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```
**Example 2:**
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```
**Note:**
1. You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
2. Input words contain only lowercase letters.
**Follow up:**
1. Try to solve it in O(n log k) time and O(n) extra space.
### Java Solution
```java
public List<String> topKFrequent(String[] words, int k) {
    Map<String, Integer> map = new HashMap<>();

    for(String c : words){
        map.putIfAbsent(c, 0);
        map.put(c, map.get(c) + 1);
    }

    map = map.entrySet().stream().sorted((e1, e2) ->
    e2.getValue() == e1.getValue() ? e1.getKey().compareTo(e2.getKey()) : e2.getValue() - e1.getValue())
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue,
            (e1, e2) -> e1, LinkedHashMap::new));

    List<String> result = new LinkedList<>();

    for(Map.Entry<String, Integer> entry : map.entrySet()){
        if(result.size() < k)
            result.add(entry.getKey());
        else
            break;
    }
    return result;
}
```