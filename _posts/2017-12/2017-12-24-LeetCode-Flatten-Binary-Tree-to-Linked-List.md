---
layout: post
title: LeetCode - Flatten Binary Tree to Linked List
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
Given a binary tree, flatten it to a linked list in-place.
<!--more-->

For example,
Given
```
         1
        / \
       2   5
      / \   \
     3   4   6
```
The flattened tree should look like:
```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```
**Hints:**

If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.->5->6->7 -> NULL

### Java Solution
```java
```