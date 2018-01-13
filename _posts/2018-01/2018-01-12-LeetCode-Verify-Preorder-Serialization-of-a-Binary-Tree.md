---
layout: post
title: LeetCode - Verify Preorder Serialization of a Binary Tree
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
One way to serialize a binary tree is to use pre-order traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as #.
```
     _9_
    /   \
   3     2
  / \   / \
 4   1  #  6
/ \ / \   / \
# # # #   # #
```
For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where # represents a null node.

Given a string of comma separated values, verify whether it is a correct preorder traversal serialization of a binary tree. Find an algorithm without reconstructing the tree.

Each comma separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid, for example it could never contain two consecutive commas such as "1,,3".
<!--more-->

**Example 1:**
"9,3,4,#,#,1,#,#,2,#,6,#,#"
Return true

**Example 2:**
"1,#"
Return false

**Example 3:**
"9,#,#,1"
Return false
### Java Solution
```java
public boolean isValidSerialization(String preorder) {
    if(preorder.equals("#")) return true;
    String[] array = preorder.split(",");
    Deque<Boolean> deque = new ArrayDeque<>();

    for(String node : array){
        if(node.equals("#")){
            if(deque.isEmpty()) return false;
            while(!deque.isEmpty() && deque.peek()){
                deque.poll();
                if(deque.isEmpty()) return false;
                deque.poll();
            }
            deque.push(true);
        }else
            deque.push(false);
    }
    return deque.size() == 1 && deque.peek();
    }
```