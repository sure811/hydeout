---
layout: post
title: LeetCode - Delete Node in a BST
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.
<!--more-->

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Note:** Time complexity should be O(height of tree).

**Example:**
```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```
### Java Solution
```java
public TreeNode deleteNode(TreeNode root, int key) {
    TreeNode parent = null;
    TreeNode node = root;
    while(node != null && node.val != key){
        parent = node;
        if(node.val > key)
            node = node.left;
        else
            node = node.right;
    }
    node = deleteNode(node);
    if(parent == null)
        return node;
    else{
        if(parent.val > key)
            parent.left = node;
        else
            parent.right = node;
    }

    return root;
}

private TreeNode deleteNode(TreeNode node) {
    if(node == null)
        return null;
    if(node.right != null){
        TreeNode parent = node;
        TreeNode newNode = node.right;
        while(newNode.left != null){
            parent = newNode;
            newNode = newNode.left;
        }
        if(newNode == node.right){
            node.right.left = node.left;
        }else{
            parent.left = newNode.right;
            newNode.left = node.left;
            newNode.right = node.right;
        }
        return newNode;
    }else if(node.left != null){
        TreeNode parent = node;
        TreeNode newNode = node.left;
        while(newNode.right != null){
            parent = newNode;
            newNode = newNode.right;
        }
        if(newNode == node.left){
            node.left.right = node.right;
        }else{
            parent.right = newNode.left;
            newNode.right = node.right;
            newNode.left = node.left;
        }
        return newNode;
    }
    return null;
}
```