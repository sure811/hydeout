---
layout: post
title: LeetCode - Binary Tree Zigzag Level Order Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).
<!--more-->

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```
### Java Solution
```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    Deque<TreeNode> stack = new ArrayDeque<>();
    List<List<Integer>> result = new ArrayList<>();
    if(root == null) return result;
    stack.push(root);
    boolean reverse = false;
    while(!stack.isEmpty()){
        int count = stack.size();
        List<Integer> level = new ArrayList<>();
        Deque<TreeNode> temp = new ArrayDeque<>();
        while(!stack.isEmpty()){
            TreeNode top = stack.pop();
            if(reverse)
                level.add(0, top.val);
            else
                level.add(top.val);
            if(top.left != null)
                temp.add(top.left);
            if(top.right != null)
                temp.add(top.right);
        }
        stack = temp;
        result.add(level);
        reverse = !reverse;
    }
    return result;
}
```