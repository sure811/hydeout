---
layout: post
title: LeetCode - Count Complete Tree Nodes
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a complete binary tree, count the number of nodes.
### Java Solution
```java
public int countNodes(TreeNode root) {
    int leftDepth = leftDepth(root);
    int rightDepth = rightDepth(root);

    if (leftDepth == rightDepth)
        return (1 << leftDepth) - 1;
    else
        return 1+countNodes(root.left) + countNodes(root.right);
}

private int rightDepth(TreeNode root) {
    int dep = 0;
    while (root != null) {
        root = root.right;
        dep++;
    }
    return dep;
}

private int leftDepth(TreeNode root) {
    int dep = 0;
    while (root != null) {
        root = root.left;
        dep++;
    }
    return dep;
}
```