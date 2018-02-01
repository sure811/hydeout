---
layout: post
title: LeetCode - Top K Frequent Elements
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-empty array of integers, return the k most frequent elements.

For example,
Given `[1,1,1,2,2,3]` and k = 2, return `[1,2]`.

**Note:**
* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
### Java Solution
```java
public List<Integer> topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();

    for(int c : nums){
        map.putIfAbsent(c, 0);
        map.put(c, map.get(c) + 1);
    }

    map = map.entrySet().stream().sorted((e1, e2) ->
    e2.getValue() - e1.getValue())
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue,
            (e1, e2) -> e1, LinkedHashMap::new));

    List<Integer> result = new LinkedList<>();

    for(Map.Entry<Integer, Integer> entry : map.entrySet()){
        if(result.size() < k)
            result.add(entry.getKey());
        else
            break;
    }
    return result;
}
```