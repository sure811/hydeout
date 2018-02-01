---
layout: post
title: LeetCode - Binary Tree Inorder Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return the inorder traversal of its nodes' values.
<!--more-->
For example:
Given binary tree `[1,null,2,3]`,
```
   1
    \
     2
    /
   3
```
return `[1,3,2]`.

**Note: **Recursive solution is trivial, could you do it iteratively?
### Java Solution
```java
public List<Integer> inorderTraversal(TreeNode root) {
    Deque<TreeNode> deque = new ArrayDeque<>();
    while(root != null){
        deque.push(root);
        root = root.left;
    }
    List<Integer> result = new LinkedList<>();
    while(!deque.isEmpty()){
        root = deque.poll();
        result.add(root.val);
        if(root.right != null){
            deque.push(root.right);
            root = root.right.left;
            while(root != null){
                deque.push(root);
                root = root.left;
            }
        }
    }
    return result;
}
```