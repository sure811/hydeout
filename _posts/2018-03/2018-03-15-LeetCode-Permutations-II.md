---
layout: post
title: LeetCode - Permutations II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a collection of numbers that might contain duplicates, return all possible unique permutations.
<!--more-->
For example,
[1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

### Java Solution
```java
public List<List<Integer>> permuteUnique(int[] nums) {
    //Arrays.sort(nums);
    boolean[] visited = new boolean[nums.length];
    List<Integer> cur = new LinkedList<>();
    Set<List<Integer>> result = new HashSet<>();
    helper(nums, visited, cur, result);
    List<List<Integer>> res = new LinkedList<>();
    res.addAll(result);
    return res;
}

private void helper(int[] nums, boolean[] visited, List<Integer> cur, Set<List<Integer>> result){
    if(cur.size() == nums.length){
        result.add(new LinkedList<>(cur));
        return;
    }
    for(int i = 0; i < nums.length; i++) {
        if(!visited[i]){
            visited[i] = true;
            cur.add(nums[i]);
            helper(nums, visited, cur, result);
            cur.remove(cur.size() - 1);
            visited[i] = false;
        }
    }
}
```