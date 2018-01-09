---
layout: post
title: LeetCode - Permutations II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a collection of numbers that might contain duplicates, return all possible unique permutations.
<!--more-->

For example,
`[1,1,2]` have the following unique permutations:
```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```
### Java Solution
```java
public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> result = new LinkedList<>();
    if(nums.length == 0) return result;
    List<Integer> cur = new LinkedList<>();
    Arrays.sort(nums);
    boolean[] visited = new boolean[nums.length];
    permuteUniqueHelper(nums, 0, visited, cur, result);
    return result;
}

private void permuteUniqueHelper(int[] nums, int level, boolean[] visited, List<Integer> cur, List<List<Integer>> result){
    if(level >= nums.length){
        result.add(new LinkedList<>(cur));
        return;
    }

    for(int i = 0; i < nums.length; i++){
        if(visited[i] || (i > 0 && nums[i] == nums[i - 1] && visited[i - 1]))
            continue;
        cur.add(nums[i]);
        visited[i] = true;
        permuteUniqueHelper(nums, level + 1, visited, cur, result);
        visited[i] = false;
        cur.remove(cur.size() - 1);
    }
}
```