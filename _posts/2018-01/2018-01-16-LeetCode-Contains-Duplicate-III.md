---
layout: post
title: LeetCode - Contains Duplicate III
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Binary Search Tree
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between `nums[i] and nums[j]` is at most t and the absolute difference between i and j is at most k.
<!--more-->
### Java Solution
```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        //input check
        if(k<1 || t<0 || nums==null || nums.length<2) return false;

        SortedSet<Long> set = new TreeSet<Long>();

        for(int j=0; j<nums.length; j++) {
            SortedSet<Long> subSet =  set.subSet((long)nums[j]-t, (long)nums[j]+t+1);
            if(!subSet.isEmpty()) return true;

            if(j>=k) {
                set.remove((long)nums[j-k]);
            }
            set.add((long)nums[j]);
        }
        return false;
    }
}
```