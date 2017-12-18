---
layout: post
title: LeetCode - Combination Sum II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.
<!--more-->

For example,

Consider the following matrix:
```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```
Given target = 3, return true.
### Java Solution
```java
public List<List<Integer>> combinationSum2(int[] candidates, int target) {
    Arrays.sort(candidates);
    boolean[] loc = new boolean[candidates.length];
    List<List<Integer>> result = new LinkedList<>();
    combinationSum2Helper(candidates, loc, 0, target, result);
    return result;
}

public void combinationSum2Helper(int[] candidates, boolean[] loc, int start, int target, List<List<Integer>> result) {
    if(target == 0){
        List<Integer> temp = new LinkedList<>();
        for(int i = 0; i < loc.length; i++)
            if(loc[i])
                temp.add(candidates[i]);
        result.add(temp);
        return;
    }
    for(int i = start; i < candidates.length; i++){
        if(candidates[i] > target)
            break;
        if(loc[i] || (i != start && candidates[i] == candidates[i - 1]))
            continue;
        loc[i] = true;
        combinationSum2Helper(candidates, loc, i + 1, target - candidates[i], result);
        loc[i] = false;
    }
}
```
