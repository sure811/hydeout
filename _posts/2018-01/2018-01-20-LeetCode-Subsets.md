---
layout: post
title: LeetCode - Subsets
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a set of distinct integers, nums, return all possible subsets (the power set).

**Note: **The solution set must not contain duplicate subsets.
<!--more-->

For example,
If nums = `[1,2,3]`, a solution is:
```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
### Java Solution
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new LinkedList<>();
        List<Integer> cur = new LinkedList<>();
        result.add(new LinkedList<>());

        for(int i = 1; i <= nums.length; i++){
            dfs(nums, 0, i, cur, result);
        }
        return result;
    }

    private void dfs(int[] nums, int start, int length, List<Integer> cur, List<List<Integer>> result){
        if(length == 0){
            result.add(new LinkedList<>(cur));
        }
        for(int i = start; i < nums.length; i++){
            if(i > start && nums[i] == nums[i - 1]) continue;
            cur.add(nums[i]);
            dfs(nums, i + 1, length - 1, cur, result);
            cur.remove(cur.size() - 1);
        }
    }
}
```