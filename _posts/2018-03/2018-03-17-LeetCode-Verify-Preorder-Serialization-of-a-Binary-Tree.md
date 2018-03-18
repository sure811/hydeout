---
layout: post
title: LeetCode - Verify Preorder Serialization of a Binary Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
<!--more-->
For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where # represents a null node.

Given a string of comma separated values, verify whether it is a correct preorder traversal serialization of a binary tree. Find an algorithm without reconstructing the tree.

Each comma separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid, for example it could never contain two consecutive commas such as "1,,3".

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
    Deque<String> stack = new ArrayDeque<>();
    String[] nodes = preorder.split(",");
    for(String node : nodes){
        stack.push(node);
        while(!stack.isEmpty()){
            String last = stack.pop();
            if(!stack.isEmpty() && stack.peek().equals("#") && last.equals("#")){
                stack.pop();
                if(stack.isEmpty() || stack.peek().equals("#"))
                    return false;
                stack.pop();
                stack.push("#");
            }else{
                stack.push(last);
                break;
            }
        }
    }
    return stack.size() == 1 && stack.peek().equals("#");
}
```