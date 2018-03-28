---
layout: post
title: LeetCode - Populating Next Right Pointers in Each Node II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?
<!--more-->
**Note:**

* You may only use constant extra space.

For example,
Given the following binary tree,
```
         1
       /  \
      2    3
     / \    \
    4   5    7
```
After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```
### Java Solution
```java
public void connect(TreeLinkNode root) {
    if(root == null) return;
    Queue<TreeLinkNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    TreeLinkNode pre = null;
    while(!queue.isEmpty()) {
        TreeLinkNode cur = queue.poll();
        if(cur == null){
            if(queue.isEmpty()) break;
            queue.offer(null);
            cur = queue.poll();
            pre.next = null;
        }else if(pre != null){
            pre.next = cur;
        }
        pre = cur;
        if(cur.left != null)
            queue.offer(cur.left);
        if(cur.right != null)
            queue.offer(cur.right);
    }
}
```