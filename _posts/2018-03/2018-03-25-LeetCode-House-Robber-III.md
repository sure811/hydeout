---
layout: post
title: LeetCode - House Robber III
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.
<!--more-->
**Example 1:**
```
     3
    / \
   2   3
    \   \
     3   1
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```
**Example 2:**
```
     3
    / \
   4   5
  / \   \
 1   3   1
Maximum amount of money the thief can rob = 4 + 5 = 9.
```
### Java Solution
```java
public int rob(TreeNode root) {
    Map<TreeNode, Integer> map = new HashMap<>();
    return dfs(root, map);
}

private int dfs(TreeNode root, Map<TreeNode, Integer> map) {
    if (root == null) return 0;
    if (map.containsKey(root)) return map.get(root);
    int val = 0;
    if (root.left != null) {
        val += dfs(root.left.left, map) + dfs(root.left.right, map);
    }
    if (root.right != null) {
        val += dfs(root.right.left, map) + dfs(root.right.right, map);
    }
    val = Math.max(val + root.val, dfs(root.left, map) + dfs(root.right, map));
    map.put(root, val);
    return val;
}
```