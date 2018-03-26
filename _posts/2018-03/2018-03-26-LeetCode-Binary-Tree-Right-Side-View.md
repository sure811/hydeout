---
layout: post
title: LeetCode - Binary Tree Right Side View
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.
<!--more-->
For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
You should return `[1, 3, 4]`.
### Java Solution
```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new LinkedList<>();
    if(root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    while(!queue.isEmpty()){
        TreeNode cur = queue.poll();
        if(cur == null){
            if(queue.isEmpty()) break;
            queue.offer(null);
            cur = queue.poll();
        }
        if(queue.peek() == null) result.add(cur.val);
        if(cur.left != null) queue.offer(cur.left);
        if(cur.right != null) queue.offer(cur.right);
    }
    return result;
}
```