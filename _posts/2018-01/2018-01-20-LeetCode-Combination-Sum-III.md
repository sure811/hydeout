---
layout: post
title: LeetCode - Combination Sum III
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.
<!--more-->

**Example 1:**
```
Input: k = 3, n = 7

Output:

[[1,2,4]]
```
**Example 2:**
```
Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]
```
### My Java Solution
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new LinkedList<>();
        List<Integer> cur = new LinkedList<>();
        dfs(k, n, 1, cur, result);
        return result;
    }

    private void dfs(int k, int n, int start, List<Integer> cur, List<List<Integer>> result){
        if(k < 0 || n < 0 || (k == 1 && n > 9)) return;

        if(k == 0 && n == 0) {
            result.add(new LinkedList<>(cur));
            return;
        }

        for(int i = start; i <= 9; i++){
            cur.add(i);
            dfs(k - 1, n - i, i + 1, cur, result);
            cur.remove(cur.size() - 1);
        }
    }
}
```