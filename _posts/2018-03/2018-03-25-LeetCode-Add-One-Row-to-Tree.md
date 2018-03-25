---
layout: post
title: LeetCode - Add One Row to Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given the root of a binary tree, then value v and depth d, you need to add a row of nodes with value v at the given depth d. The root node is at depth 1.

The adding rule is: given a positive integer depth d, for each NOT null tree nodes N in depth d-1, create two tree nodes with value v as N's left subtree root and right subtree root. And N's original left subtree should be the left subtree of the new left subtree root, its original right subtree should be the right subtree of the new right subtree root. If depth d is 1 that means there is no depth d-1 at all, then create a tree node with value v as the new root of the whole original tree, and the original tree is the new root's left subtree.
<!--more-->
**Example 1:**
```
Input:
A binary tree as following:
       4
     /   \
    2     6
   / \   /
  3   1 5

v = 1

d = 2

Output:
       4
      / \
     1   1
    /     \
   2       6
  / \     /
 3   1   5
```
**Example 2:**
```
Input:
A binary tree as following:
      4
     /
    2
   / \
  3   1

v = 1

d = 3

Output:
      4
     /
    2
   / \
  1   1
 /     \
3       1
```
**Note:**
1. The given d is in range `[1, maximum depth of the given tree + 1]`.
2. The given binary tree has at least one tree node.
### Java Solution
```java
public TreeNode addOneRow(TreeNode root, int v, int d) {
    if(d == 1){
        TreeNode newRoot = new TreeNode(v);
        newRoot.left = root;
        return newRoot;
    }
    if(root == null) return root;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while(!queue.isEmpty()){
        int size = queue.size();
        if(--d == 1){
            for(int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                if(node.left != null){
                    TreeNode newNode = new TreeNode(v);
                    newNode.left = node.left;
                    node.left = newNode;
                }else{
                    TreeNode newNode = new TreeNode(v);
                    node.left = newNode;
                }

                if(node.right != null){
                    TreeNode newNode = new TreeNode(v);
                    newNode.right = node.right;
                    node.right = newNode;
                }else{
                    TreeNode newNode = new TreeNode(v);
                    node.right = newNode;
                }
            }
            return root;
        }
        for(int i = 0; i < size; i++){
            TreeNode node = queue.poll();
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
    }
    return root;
}
```