---
layout: post
title: LeetCode - Print Binary Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Print a binary tree in an m*n 2D string array following these rules:

1. The row number m should be equal to the height of the given binary tree.
2. The column number n should always be an odd number.
3. The root node's value (in string format) should be put in the exactly middle of the first row it can be put. The column and the row where the root node belongs will separate the rest space into two parts (left-bottom part and right-bottom part). You should print the left subtree in the left-bottom part and print the right subtree in the right-bottom part. The left-bottom part and the right-bottom part should have the same size. Even if one subtree is none while the other is not, you don't need to print anything for the none subtree but still need to leave the space as large as that for the other subtree. However, if two subtrees are none, then you don't need to leave space for both of them.
4. Each unused space should contain an empty string "".
5. Print the subtrees following the same rules.
<!--more-->
**Example 1:**
```
Input:
     1
    /
   2
Output:
[["", "1", ""],
 ["2", "", ""]]
```
**Example 2:**
```
Input:
     1
    / \
   2   3
    \
     4
Output:
[["", "", "", "1", "", "", ""],
 ["", "2", "", "", "", "3", ""],
 ["", "", "4", "", "", "", ""]]
```
**Example 3:**
```
Input:
      1
     / \
    2   5
   /
  3
 /
4
Output:

[["",  "",  "", "",  "", "", "", "1", "",  "",  "",  "",  "", "", ""]
 ["",  "",  "", "2", "", "", "", "",  "",  "",  "",  "5", "", "", ""]
 ["",  "3", "", "",  "", "", "", "",  "",  "",  "",  "",  "", "", ""]
 ["4", "",  "", "",  "", "", "", "",  "",  "",  "",  "",  "", "", ""]]
```
**Note: **The height of binary tree is in the range of `[1, 10]`.
### Java Solution
```java
class Solution {
    public List<List<String>> printTree(TreeNode root) {
        int h = getHeight(root), w = (int)Math.pow(2, h) - 1;
        List<List<String>> result = new LinkedList<>();
        for(int i = 0; i < h; i++){
            List<String> cur = new LinkedList<>();
            for(int j = 0; j < w; j++)
                cur.add("");
            result.add(cur);
        }
        helper(root, 0, w - 1, 0, h, result);
        return result;
    }
    void helper(TreeNode node, int i, int j, int curH, int height, List<List<String>> result) {
        if (node == null || curH == height) return;
        result.get(curH).set((i + j) / 2, Integer.toString(node.val));
        helper(node.left, i, (i + j) / 2, curH + 1, height, result);
        helper(node.right, (i + j) / 2 + 1, j, curH + 1, height, result);
    }

    private int getHeight(TreeNode node) {
        if (node == null) return 0;
        return 1 + Math.max(getHeight(node.left), getHeight(node.right));
    }
}
```