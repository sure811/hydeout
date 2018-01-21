---
layout: post
title: LeetCode - Combination Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a set of candidate numbers (C) (without duplicates) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.
<!--more-->

**Note:**
* All numbers (including target) will be positive integers.
* The solution set must not contain duplicate combinations.
For example, given candidate set `[2, 3, 6, 7]` and target 7,
A solution set is:
```
[
  [7],
  [2, 2, 3]
]
```
### My Java Solution
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
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
            cur.add(candidates[i]);
            dfs(candidates, target - candidates[i], i, cur, result);
            cur.remove(cur.size() - 1);
        }
    }
}
```