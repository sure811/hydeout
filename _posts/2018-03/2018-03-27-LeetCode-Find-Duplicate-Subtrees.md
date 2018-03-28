---
layout: post
title: LeetCode - Find Duplicate Subtrees
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.
<!--more-->
**Example 1: **
```
        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
```
The following are two duplicate subtrees:
```
      2
     /
    4
```
and
```
    4
```
Therefore, you need to return above trees' root in the form of a list.
### Java Solution
```java
public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
    List<TreeNode> res = new LinkedList<>();
    Map<String, Integer> m = new HashMap<>();
    helper(root, m, res);
    return res;
}
private String helper(TreeNode node, Map<String, Integer> m, List<TreeNode> res) {
    if (node == null) return "#";
    String str = Integer.toString(node.val) + "," + helper(node.left, m, res) + "," + helper(node.right, m, res);
    m.putIfAbsent(str, 0);
    if (m.get(str) == 1) res.add(node);
    m.put(str, m.get(str) + 1);
    return str;
}
```