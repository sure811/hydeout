---
layout: post
title: LeetCode - Validate Binary Search Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
<!--more-->
**Example 1:**
```
    2
   / \
  1   3
```
Binary tree `[2,1,3]`, return true.
**Example 2:**
```
    1
   / \
  2   3
```
Binary tree `[1,2,3]`, return false.
### Java Solution
```java
public boolean isValidBST(TreeNode root) {
    return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

private boolean isValidBST(TreeNode root, long left, long right) {
    if(root == null) return true;
    if(root.val <= left || root.val >= right) return false;
    if(root.left == null && root.right == null){
        return true;
    }
    return isValidBST(root.left, left, root.val) && isValidBST(root.right, root.val, right);
}
```