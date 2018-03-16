---
layout: post
title: LeetCode - Combinations
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
<!--more-->
For example,
If n = 4 and k = 2, a solution is:
```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```
### Java Solution
```java
public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> result = new LinkedList<>();
    List<Integer> cur = new LinkedList<>();
    helper(n, k, 1, cur, result);
    return result;
}

private void helper(int n, int k, int start, List<Integer> cur, List<List<Integer>> result){
    if(k == 0){
        result.add(new LinkedList<>(cur));
        return;
    }
    for(int i = start; i <= n; i++){
        cur.add(i);
        helper(n, k - 1, i + 1, cur, result);
        cur.remove(cur.size() - 1);
    }
}
```