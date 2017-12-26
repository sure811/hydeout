---
layout: post
title: LeetCode - Populating Next Right Pointers in Each Node II
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
Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

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
    TreeLinkNode dummy = new TreeLinkNode(0);
    TreeLinkNode t = dummy;
    while (root != null) {
        if (root.left != null) {
            t.next = root.left;
            t = t.next;
        }
        if (root.right != null) {
            t.next = root.right;
            t = t.next;
        }
        root = root.next;
        if (root == null) {
            t = dummy;
            root = dummy.next;
            dummy.next = null;
        }
    }
}
```