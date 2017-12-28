---
layout: post
title: LeetCode - Binary Tree Zigzag Level Order Traversal
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Tree
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
    List<List<Integer>> result = new LinkedList<>();
    if(root == null) return result;

    Deque<TreeNode> stack1 = new ArrayDeque<>();
    Deque<TreeNode> stack2 = new ArrayDeque<>();
    stack1.push(root);
    while(!stack1.isEmpty() || !stack2.isEmpty()){
        List<Integer> level = new LinkedList<>();
        if(!stack1.isEmpty()){
            while(!stack1.isEmpty()){
                TreeNode node = stack1.pop();
                if(node.left != null)
                    stack2.push(node.left);
                if(node.right != null)
                    stack2.push(node.right);
                level.add(node.val);
            }
        }else{
            while(!stack2.isEmpty()){
                TreeNode node = stack2.pop();
                if(node.right != null)
                    stack1.push(node.right);
                if(node.left != null)
                    stack1.push(node.left);
                level.add(node.val);
            }
        }
        result.add(level);
    }
    return result;
}
```