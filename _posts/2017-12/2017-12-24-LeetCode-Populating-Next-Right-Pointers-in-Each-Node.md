---
layout: post
title: LeetCode - Populating Next Right Pointers in Each Node
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
    - Depth First Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree
```
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.
<!--more-->

**Note:**

You may only use constant extra space.
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
For example,
Given the following perfect binary tree,
```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```
### Java Solution
```java
public void connect(TreeLinkNode root) {
    if(root == null)
        return;
    Queue<TreeLinkNode> queue = new LinkedList<>();
    queue.add(root);
    queue.add(null);
    TreeLinkNode pre = null;
    while(!queue.isEmpty()){
        TreeLinkNode node = queue.poll();
        if(node == null){
            pre = null;
            if(!queue.isEmpty())
                queue.add(null);
            continue;
        }
        if(node.left != null)
            queue.add(node.left);
        if(node.right != null)
            queue.add(node.right);
        if(pre != null){
            pre.next = node;
        }
        pre = node;
    }
}
```