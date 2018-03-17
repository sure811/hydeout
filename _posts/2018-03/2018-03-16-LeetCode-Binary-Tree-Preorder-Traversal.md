---
layout: post
title: LeetCode - Binary Tree Preorder Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree `[1,null,2,3]`,
```
   1
    \
     2
    /
   3
```
return `[1,2,3]`.

**Note:** Recursive solution is trivial, could you do it iteratively?
### Java Solution
```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new LinkedList<>();
    if(root == null) return result;

    Deque<TreeNode> deque = new ArrayDeque<>();
    deque.push(root);

    while(!deque.isEmpty()){
        TreeNode temp = deque.pop();
        result.add(temp.val);
        if(temp.right != null) deque.push(temp.right);
        if(temp.left != null) deque.push(temp.left);
    }
    return result;
}
```