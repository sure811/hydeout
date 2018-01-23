---
layout: post
title: LeetCode - Construct Binary Tree from Inorder and Postorder Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
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
    return buildTree(inorder, postorder, 0, inorder.length - 1, inorder.length - 1);
}

private TreeNode buildTree(int[] inorder, int[] postorder, int start, int end, int rootIndex){
    if(start > end) return null;
    TreeNode root = new TreeNode(postorder[rootIndex]);
    int newRoot = -1;
    for(int i = start; i <= end; i++){
        if(inorder[i] == postorder[rootIndex]){
            newRoot = i;
            break;
        }
    }
    root.left = buildTree(inorder, postorder, start, newRoot - 1, rootIndex - end + newRoot - 1);
    root.right = buildTree(inorder, postorder, newRoot + 1, end, rootIndex - 1);
    return root;
}
```