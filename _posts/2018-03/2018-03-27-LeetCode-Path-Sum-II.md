---
layout: post
title: LeetCode - Path Sum II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and sum = 22,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```
### Java Solution
```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        if(root == null) return new LinkedList<>();
        List<List<Integer>> result = new LinkedList<>();
        List<Integer> cur = new LinkedList<>();
        dfs(root, sum, cur, result);
        return result;
    }

    private void dfs(TreeNode root, int sum, List<Integer> cur, List<List<Integer>> result) {
        if(root == null){
            return;
        }
        cur.add(root.val);
        if(root.left == null && root.right == null && root.val == sum){
            result.add(new LinkedList<>(cur));
            cur.remove(cur.size() - 1);
            return;
        }
        dfs(root.left, sum - root.val, cur, result);
        dfs(root.right, sum - root.val, cur, result);
        cur.remove(cur.size() - 1);
    }
}
```