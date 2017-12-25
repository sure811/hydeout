---
layout: post
title: LeetCode - Path Sum II
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
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
<!--more-->
For example:
Given the below binary tree and sum = 22,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```
### Java Solution
```java
public List<List<Integer>> pathSum(TreeNode root, int sum) {
    List<List<Integer>> result = new LinkedList<>();
    if(root == null)
        return result;
    List<Integer> cur = new LinkedList<>();
    pathSumHelper(root, cur, result, sum);
    return result;
}

public void pathSumHelper(TreeNode root, List<Integer> cur, List<List<Integer>> result, int sum) {
    if(root.left == null && root.right == null){
        if(sum == root.val){
            cur.add(root.val);
            result.add(new LinkedList(cur));
            cur.remove(cur.size() - 1);
        }
        return;
    }
    cur.add(root.val);
    if(root.left != null){
        pathSumHelper(root.left, cur, result, sum - root.val);
    }
    if(root.right != null){
        pathSumHelper(root.right, cur, result, sum - root.val);
    }
    cur.remove(cur.size() - 1);
}
```