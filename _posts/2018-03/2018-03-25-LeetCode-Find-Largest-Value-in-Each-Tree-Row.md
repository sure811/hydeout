---
layout: post
title: LeetCode - Find Largest Value in Each Tree Row
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
You need to find the largest value in each row of a binary tree.
<!--more-->
**Example:**
```
Input:

          1
         / \
        3   2
       / \   \
      5   3   9

Output: [1, 3, 9]
```
### Java Solution
```java
public List<Integer> largestValues(TreeNode root) {
    List<Integer> result = new LinkedList<>();
    if(root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while(!queue.isEmpty()){
        int size = queue.size();
        int max = Integer.MIN_VALUE;
        for(int i = 0; i < size; i++){
            TreeNode node = queue.poll();
            max = Math.max(max, node.val);
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
        result.add(max);
    }
    return result;
}
```