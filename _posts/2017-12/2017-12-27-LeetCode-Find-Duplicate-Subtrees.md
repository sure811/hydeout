---
layout: post
title: LeetCode - Find Duplicate Subtrees
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return all duplicate subtrees. For each kind of duplicate subtrees, you only need to return the root node of any one of them.

Two trees are duplicate if they have the same structure with same node values.
<!--more-->

**Example 1:**
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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        List<TreeNode> result = new LinkedList<>();
        Map<String, Integer> map = new HashMap<>();
        helper(root, map, result);
        return result;
    }

    private String helper(TreeNode node, Map<String, Integer>map, List<TreeNode> result) {
        if (node == null) return "#";
        String str = Integer.toString(node.val) + "," + helper(node.left, map, result) + "," + helper(node.right, map, result);
        if (map.containsKey(str) && map.get(str) == 1) result.add(node);
        map.putIfAbsent(str, 0);
        map.put(str, map.get(str) + 1);
        return str;
    }
}
```