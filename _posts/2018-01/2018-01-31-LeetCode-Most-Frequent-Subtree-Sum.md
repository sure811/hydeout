---
layout: post
title: LeetCode - Most Frequent Subtree Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.
<!--more-->
**Examples 1**
```
Input:

  5
 /  \
2   -3
return [2, -3, 4], since all the values happen only once, return all of them in any order.
```
**Examples 2**
```
Input:

  5
 /  \
2   -5
return [2], since 2 happens twice, however -5 only occur once.
```
**Note: **You may assume the sum of values in any subtree is in the range of 32-bit signed integer.
### Java Solution
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] findFrequentTreeSum(TreeNode root) {
        Map<Integer, Integer> map = new HashMap<>();
        getTreeSum(root, map);
        int max = 0;
        List<Integer> result = new LinkedList<>();
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() > max){
                max = entry.getValue();
                result = new LinkedList<>();
                result.add(entry.getKey());
            }else if(entry.getValue() == max){
                result.add(entry.getKey());
            }
        }
        return result.stream().mapToInt(i->i).toArray();
    }

    private int getTreeSum(TreeNode root, Map<Integer, Integer> map){
        if(root == null) return 0;
        int left = getTreeSum(root.left, map);
        int right = getTreeSum(root.right, map);
        int sum = root.val + left + right;
        map.putIfAbsent(sum, 0);
        map.put(sum, map.get(sum) + 1);
        return sum;
    }
}
```