---
layout: post
title: LeetCode - Unique Binary Search Trees II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.
<!--more-->

For example,
Given n = 3, your program should return all 5 unique BST's shown below.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
### Java Solution
```java
public List<TreeNode> generateTrees(int n) {
    if(n == 0)
        return new LinkedList<>();
    return genTrees(1,n);
}

public List<TreeNode> genTrees (int start, int end)
{

    List<TreeNode> list = new ArrayList<TreeNode>();

    if(start>end)
    {
        list.add(null);
        return list;
    }

    if(start == end){
        list.add(new TreeNode(start));
        return list;
    }

    List<TreeNode> left,right;
    for(int i=start;i<=end;i++)
    {

        left = genTrees(start, i-1);
        right = genTrees(i+1,end);

        for(TreeNode lnode: left)
        {
            for(TreeNode rnode: right)
            {
                TreeNode root = new TreeNode(i);
                root.left = lnode;
                root.right = rnode;
                list.add(root);
            }
        }

    }

    return list;
}
```