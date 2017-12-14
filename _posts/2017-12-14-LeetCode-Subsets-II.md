---
layout: post
title: LeetCode - Subsets II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Combination
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).
<!--more-->

**Note:** The solution set must not contain duplicate subsets.

For example,
If nums = `[1,2,2]`, a solution is:
```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
### Java Solution
```java
class Solution {
    List<List<Integer>> list;
    List<Integer> al;

    public List<List<Integer>> subsetsWithDup(int[] nums) {
        list = new ArrayList<List<Integer>>();
        al = new ArrayList<Integer>();
        Arrays.sort(nums);
        count(nums,al,0);
        return list;
    }

    private void count(int[] nums,List<Integer> al,int j){

    	list.add(new ArrayList<Integer>(al));

        for(int i = j; i < nums.length;i++){
        	if(i == j || nums[i] != nums[i-1]){
        		al.add(nums[i]);
                count(nums,al,i+1);
                al.remove(al.size()-1);
        	}
        }
    }
}
```
