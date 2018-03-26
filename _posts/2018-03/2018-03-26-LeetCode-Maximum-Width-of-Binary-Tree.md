---
layout: post
title: LeetCode - Maximum Width of Binary Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a full binary tree, but some nodes are null.

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the null nodes between the end-nodes are also counted into the length calculation.
<!--more-->
**Example 1:**
```
Input:

           1
         /   \
        3     2
       / \     \
      5   3     9

Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```
**Example 2:**
```
Input:

          1
         /
        3
       / \
      5   3

Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```
**Example 3:**
```
Input:

          1
         / \
        3   2
       /
      5

Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```
**Example 4:**
```
Input:

          1
         / \
        3   2
       /     \
      5       9
     /         \
    6           7
Output: 8
Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

**Note:** Answer will in the range of 32-bit signed integer.
### Java Solution
```java
public int widthOfBinaryTree(TreeNode root) {
    int res = 0;
    List<Integer> start = new LinkedList();
    return helper(root, 0, 1, start, 0);
}
private int helper(TreeNode node, int h, int idx, List<Integer> start, int res) {
    if (node == null) return res;
    if (h >= start.size()) start.add(idx);
    res = Math.max(res, idx - start.get(h) + 1);
    res = Math.max(res, helper(node.left, h + 1, idx * 2, start, res));
    res = Math.max(res, helper(node.right, h + 1, idx * 2 + 1, start, res));
    return res;
}
```