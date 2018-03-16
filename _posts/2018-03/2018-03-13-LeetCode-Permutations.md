---
layout: post
title: LeetCode - Permutations
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a collection of distinct numbers, return all possible permutations.
<!--more-->

For example,
`[1,2,3]` have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
### Java Solution
```java
public List<List<Integer>> permute(int[] nums) {
    boolean[] visited = new boolean[nums.length];
    List<Integer> cur = new LinkedList<>();
    List<List<Integer>> result = new LinkedList<>();
    helper(nums, visited, cur, result);
    return result;
}

private void helper(int[] nums, boolean[] visited, List<Integer> cur, List<List<Integer>> result){
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