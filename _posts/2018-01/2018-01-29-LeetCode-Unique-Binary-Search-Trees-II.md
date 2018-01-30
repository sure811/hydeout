---
layout: post
title: LeetCode - Unique Binary Search Trees II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.
<!--more-->

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

### Java Solution
```java
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if(n == 0) return new LinkedList<>();
        return dfs(1,n);
    }

    private List<TreeNode> dfs(int left, int right){
        List<TreeNode> result = new LinkedList<>();
        if(left == right){
            result.add(new TreeNode(left));
            return result;
        }
        if(left > right){
            return null;
        }
        for(int i = left; i <= right; i++){
            List<TreeNode> lefts = dfs(left, i - 1);
            List<TreeNode> rights = dfs(i + 1, right);
            if(lefts == null){
                for(TreeNode r : rights){
                    TreeNode root = new TreeNode(i);
                    root.right = r;
                    result.add(root);
                }
            }
            else if(rights == null){
                for(TreeNode r : lefts){
                    TreeNode root = new TreeNode(i);
                    root.left = r;
                    result.add(root);
                }
            } else{
                for(TreeNode l : lefts){
                    for(TreeNode r : rights){
                        TreeNode root = new TreeNode(i);
                        root.left = l;
                        root.right = r;
                        result.add(root);
                    }
                }
            }
        }
        return result;
    }
}
```