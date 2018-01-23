---
layout: post
title: LeetCode - Construct Binary Tree from Preorder and Inorder Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given preorder and inorder traversal of a tree, construct the binary tree.
<!--more-->
**Note:**

You may assume that duplicates do not exist in the tree.
### My Java Solution
```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTree(preorder, inorder, 0, preorder.length - 1, 0);
    }

    private TreeNode buildTree(int[] preorder, int[] inorder, int start, int end, int rootIndex){
        if(start > end) return null;
        TreeNode root = new TreeNode(preorder[rootIndex]);
        int newRoot = -1;
        for(int i = start; i <= end; i++){
            if(inorder[i] == preorder[rootIndex]){
                newRoot = i;
                break;
            }
        }
        root.left = buildTree(preorder, inorder, start, newRoot - 1, rootIndex + 1);
        root.right = buildTree(preorder, inorder, newRoot + 1, end, rootIndex + newRoot - start + 1);
        return root;
    }
}
```