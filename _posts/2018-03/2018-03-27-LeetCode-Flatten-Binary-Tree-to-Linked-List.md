---
layout: post
title: LeetCode - Flatten Binary Tree to Linked List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, flatten it to a linked list in-place.
<!--more-->

For example,
Given
```
         1
        / \
       2   5
      / \   \
     3   4   6
The flattened tree should look like:
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
click to show hints.

Hints:
If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.
### Java Solution
```java
public void flatten(TreeNode root) {
    if(root == null) return;
    flatten(root.right);
    if(root.left != null){
        TreeNode left = root.left;
        flatten(left);
        TreeNode last = left;
        while(last.right != null)
            last = last.right;
        last.right = root.right;
        root.right = left;
        root.left = null;
    }
    return;
}
```