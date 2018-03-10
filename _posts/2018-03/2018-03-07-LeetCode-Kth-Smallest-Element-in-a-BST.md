---
layout: post
title: LeetCode - Kth Smallest Element in a BST
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.
<!--more-->

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?
### Java Solution
```java
public int kthSmallest(TreeNode root, int k) {
    Stack<TreeNode> stack = new Stack<>();
    while(root != null){
        stack.push(root);
        root = root.left;
    }
    while(!stack.isEmpty()) {
        TreeNode cur = stack.pop();
        if(--k == 0) return cur.val;
        if(cur.right != null){
            cur = cur.right;
            while(cur != null){
                stack.push(cur);
                cur = cur.left;
            }
        }
    }
    return -1;
}
```