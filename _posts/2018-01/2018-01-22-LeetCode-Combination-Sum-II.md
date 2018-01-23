---
layout: post
title: LeetCode - Combination Sum II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.
<!--more-->
**Note:**

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]` and target 8,
A solution set is:
```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
### Java Solution
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> result = new LinkedList<>();
        List<Integer> cur = new LinkedList<>();
        dfs(candidates, target, 0, cur, result);
        return result;
    }
    private void dfs(int[] candidates, int target, int start, List<Integer> cur, List<List<Integer>> result){
        if(target < 0) return;
        if(target == 0){
            result.add(new LinkedList<>(cur));
            return;
        }

        for(int i = start; i < candidates.length; i++){
            if(i > start && candidates[i] == candidates[i - 1]) continue;
            cur.add(candidates[i]);
            dfs(candidates, target - candidates[i], i + 1, cur, result);
            cur.remove(cur.size() - 1);
        }
    }
}
```