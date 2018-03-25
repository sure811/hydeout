---
layout: post
title: LeetCode - Find Bottom Left Tree Value
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, find the leftmost value in the last row of the tree.
<!--more-->

**Example 1:**
```
Input:

    2
   / \
  1   3

Output:
1
```
**Example 2:**
```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```
**Note: **You may assume the tree (i.e., the given root node) is not NULL.
### Java Solution
```java
public int findBottomLeftValue(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    int result = root.val;
    while(!queue.isEmpty()){
        TreeNode cur = queue.poll();
        if(cur == null){
            if(queue.isEmpty()) break;
            queue.offer(null);
            cur = queue.poll();
            result = cur.val;
        }
        if(cur.left != null) queue.offer(cur.left);
        if(cur.right != null) queue.offer(cur.right);
    }
    return result;
}
```