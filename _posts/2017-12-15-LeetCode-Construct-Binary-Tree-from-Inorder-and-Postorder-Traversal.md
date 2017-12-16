---
layout: post
title: LeetCode - Construct Binary Tree from Inorder and Postorder Traversal
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

Given inorder and postorder traversal of a tree, construct the binary tree.
<!--more-->

**Note:**

You may assume that duplicates do not exist in the tree.

### Java Solution
```java
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return buildTreeHelper(inorder, postorder, 0, postorder.length - 1, postorder.length - 1);
    }

    public TreeNode buildTreeHelper(int[] inorder, int[] postorder, int start, int end, int index) {
        if(start > end || index < 0)
            return null;
        int rootVal = postorder[index];
        TreeNode root = new TreeNode(rootVal);
        int rootIndex = start;
        for(; rootIndex <= end; rootIndex++)
            if(inorder[rootIndex] == rootVal)
                break;
        root.left = buildTreeHelper(inorder, postorder, start, rootIndex - 1, index + rootIndex - end - 1);
        root.right = buildTreeHelper(inorder, postorder, rootIndex + 1, end, index - 1);
        return root;
    }
```
