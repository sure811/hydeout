---
layout: post
title: LeetCode - Lowest Common Ancestor of a Binary Tree
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
<!--more-->

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```
For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
### Java Solution
```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    List<TreeNode> listp = new LinkedList<>();
    List<TreeNode> listq = new LinkedList<>();
    if(!findNode(root, p, listp))
        return null;
    if(!findNode(root, q, listq))
        return null;
    TreeNode result = null;
    int i = 0;
    for(; i < listp.size() && i < listq.size() && listp.get(i) == listq.get(i); i++);
    if(i < listp.size())
        result = listp.get(i - 1);
    else if(i < listq.size())
        result = listq.get(i - 1);
    return result;
}

private boolean findNode(TreeNode root, TreeNode p, List<TreeNode> list){
    if(root == p){
        list.add(p);
        return true;
    }
    if(root == null)
        return false;
    list.add(root);
    if(findNode(root.left, p, list))
        return true;
    if(findNode(root.right, p, list))
        return true;
    list.remove(list.size() - 1);
    return false;
}
```