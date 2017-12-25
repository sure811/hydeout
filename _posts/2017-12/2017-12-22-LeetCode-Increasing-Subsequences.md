---
layout: post
title: LeetCode - Increasing Subsequences
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
    - Depth First Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .
<!--more-->

**Example:**
```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```
**Note:**
1. The length of the given array will not exceed 15.
2. The range of integer in the given array is [-100,100].
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

### Java Solution
```java
public List<List<Integer>> findSubsequences(int[] nums) {
    List<Integer> cur = new LinkedList<>();
    return new LinkedList(findSubsequencesHelper(nums, cur, 0));
}

private Set<List<Integer>> findSubsequencesHelper(int[] nums, List<Integer> cur, int start){
    Set<List<Integer>> result = new HashSet<>();
    if(cur.size() > 1){
        result.add(new LinkedList(cur));
    }

    for(int i = start; i < nums.length; i++){
        if(cur.size() > 0 && cur.get(cur.size() - 1) > nums[i])
            continue;
        cur.add(nums[i]);
        Set<List<Integer>> temp = findSubsequencesHelper(nums, cur, i + 1);
        for(List<Integer> t : temp)
            result.add(t);
        cur.remove(cur.size() - 1);
    }
    return result;
}
```