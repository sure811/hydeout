---
layout: post
title: LeetCode - Sum Root to Leaf Numbers
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
Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.
<!--more-->

For example,
```
    1
   / \
  2   3
```
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.

### Java Solution
```java
public int sumNumbers(TreeNode root) {
    return sumNumbersHelper(root, 0);
}

private int sumNumbersHelper(TreeNode root, int num) {
    if(root == null)
        return num;
    int result = 0;
    if(root.left != null)
        result += sumNumbersHelper(root.left, num * 10 + root.val);
    if(root.right != null)
        result += sumNumbersHelper(root.right, num * 10 + root.val);
    if(root.left == null && root.right == null)
        result =  num * 10 + root.val;
    return result;
}
```