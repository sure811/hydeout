---
layout: post
title: LeetCode - Binary Tree Level Order Traversal
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
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
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
### Java Solution
```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new LinkedList<>();
    if(root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    List<Integer> list = new LinkedList<>();
    while(!queue.isEmpty()){
        TreeNode cur = queue.poll();
        if(cur == null){
            if(queue.isEmpty()) break;
            queue.offer(null);
            result.add(list);
            list = new LinkedList<>();
            cur = queue.poll();
        }
        list.add(cur.val);
        if(cur.left != null) queue.offer(cur.left);
        if(cur.right != null) queue.offer(cur.right);
    }
    if(list.size() > 0) result.add(list);
    return result;
}
```