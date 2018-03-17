---
layout: post
title: LeetCode - Range Sum Query - Mutable
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

The update(i, val) function modifies nums by updating the element at index i to val.
<!--more-->

**Example:**
```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```
**Note:**
1. The array is only modifiable by the update function.
2. You may assume the number of calls to update and sumRange function is distributed evenly.
### Java Solution
```java
class NumArray {
    private TreeNode root;
    private int[] nums;
    public NumArray(int[] nums) {
        if(nums.length == 0) return;
        root = new TreeNode(nums, 0, nums.length);
        this.nums = nums;
    }

    public void update(int i, int val) {
        int change = val - nums[i];
        nums[i] = val;
        TreeNode cur = root;
        while(cur != null){
            cur.sum += change;
            if(cur.left != null && i >= cur.left.range[0] && i < cur.left.range[1]){
                cur = cur.left;
            } else if(cur.right != null && i >= cur.right.range[0] && i < cur.right.range[1]){
                cur = cur.right;
            } else
                break;
        }
    }

    public int sumRange(int i, int j) {
        return sumRange(root, i, j + 1);
    }

    private int sumRange(TreeNode cur, int i, int j){
        if(cur == null || i < cur.range[0] || j > cur.range[1])
            return -1;
        if(cur.range[0] == i && cur.range[1] == j)
            return cur.sum;
        int mid = (cur.range[0] + cur.range[1]) / 2;
        if(j <= mid)
            return sumRange(cur.left, i, j);
        if(i >= mid)
            return sumRange(cur.right, i, j);
        return sumRange(cur.left, i, mid) + sumRange(cur.right, mid, j);
    }

    class TreeNode {
        int[] range;
        int sum;
        TreeNode left;
        TreeNode right;

        TreeNode(int[] nums, int start, int end){
            this.range = new int[]{start, end};
            int mid = (start + end) / 2;
            if(start < end - 1){
                left = new TreeNode(nums, start, mid);
                right = new TreeNode(nums, mid, end);
                this.sum = left.sum + right.sum;
            }else {
                this.sum = nums[start];
            }
        }
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```