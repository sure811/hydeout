---
layout: post
title: LeetCode - Delete Node in a BST
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

Search for a node to remove.
If the node is found, delete the node.
Note: Time complexity should be O(height of tree).
<!--more-->

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
    if(root == null) return root;
    TreeNode oriRoot = root;
    TreeNode parent = root;
    if(root.val == key){
        parent = null;
    } else {
        while(root != null && root.val != key){
            parent = root;
            if(root.val > key)
                root = root.left;
            else
                root = root.right;
        }
        if(root == null) return oriRoot;
    }
    if(root.left != null){
        TreeNode newNode = root.left;
        TreeNode newNodeParent = root;
        while(newNode.right != null){
            newNodeParent = newNode;
            newNode = newNode.right;
        }
        if(newNodeParent != root){
            if(newNode.left != null)
                newNodeParent.right = newNode.left;
            else
                newNodeParent.right = null;
        }
        if(root.left != newNode)
            newNode.left = root.left;
        newNode.right = root.right;
        if(parent != null){
            if(parent.val > key)
                parent.left = newNode;
            else
                parent.right = newNode;
        }else
            return newNode;
    } else if(root.right != null){
        TreeNode newNode = root.right;
        TreeNode newNodeParent = root;
        while(newNode.left != null){
            newNodeParent = newNode;
            newNode = newNode.left;
        }
        if(newNodeParent != root){
            if(newNode.right != null)
                newNodeParent.left = newNode.right;
            else
                newNodeParent.left = null;
        }
        if(root.right != newNode)
            newNode.right = root.right;
        newNode.left = root.left;
        if(parent != null){
            if(parent.val > key)
                parent.left = newNode;
            else
                parent.right = newNode;
        }else
            return newNode;
    } else {
        if(parent != null){
            if(parent.val > key)
                parent.left = null;
            else
                parent.right = null;
        }else
            return null;
    }
    return oriRoot;
}
```