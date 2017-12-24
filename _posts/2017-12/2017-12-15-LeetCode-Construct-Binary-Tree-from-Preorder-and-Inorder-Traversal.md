---
layout: post
title: LeetCode - Construct Binary Tree from Preorder and Inorder Traversal
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition

Given preorder and inorder traversal of a tree, construct the binary tree.
<!--more-->

**Note:**

You may assume that duplicates do not exist in the tree.

### Java Solution
```java
public TreeNode buildTree(int[] preorder, int[] inorder) {
    return buildTreeHelper(preorder, inorder, 0, preorder.length - 1, 0);
}

public TreeNode buildTreeHelper(int[] preorder, int[] inorder, int start, int end, int index) {
    if(start > end || index >= preorder.length)
        return null;
    int rootVal = preorder[index];
    TreeNode root = new TreeNode(rootVal);
    int rootIndex = start;
    for(; rootIndex <= end; rootIndex++)
        if(inorder[rootIndex] == rootVal)
            break;
    root.left = buildTreeHelper(preorder, inorder, start, rootIndex - 1, index + 1);
    root.right = buildTreeHelper(preorder, inorder, rootIndex + 1, end, index + rootIndex - start + 1);
    return root;
}
```
