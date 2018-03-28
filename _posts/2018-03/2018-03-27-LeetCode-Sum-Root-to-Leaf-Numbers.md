---
layout: post
title: LeetCode - Sum Root to Leaf Numbers
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.
<!--more-->

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.
### Java Solution
```java
public int sumNumbers(TreeNode root) {
    return helper(root, 0);
}

private int helper(TreeNode root, int parent) {
    if(root == null) return parent;
    parent = parent * 10 + root.val;
    int result = 0;
    if(root.left != null)
        result += helper(root.left, parent);
    if(root.right != null)
        result += helper(root.right, parent);
    if(root.left == null && root.right == null)
        result = parent;
    return result;
}
```