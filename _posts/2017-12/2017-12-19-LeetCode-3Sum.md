---
layout: post
title: LeetCode - 3Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
<!--more-->

Note: The solution set must not contain duplicate triplets.

For example, given array S = `[-1, 0, 1, 2, -1, -4]`,
```
A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```
### Java Solution
```java
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new LinkedList<>();
    for(int i = 0; i < nums.length; i++){
        if(i > 0 && nums[i] == nums[i - 1])
            continue;
        int start = i + 1;
        int end = nums.length - 1;
        while(start < end){
            if(nums[start] + nums[end] + nums[i] == 0){
                List<Integer> temp = new LinkedList<>();
                temp.add(nums[start]);
                temp.add(nums[end]);
                temp.add(nums[i]);
                result.add(temp);
                start++;
                end--;
                while(start < nums.length && nums[start] == nums[start - 1])
                    start++;
                while(end >= 0 && nums[end] == nums[end + 1])
                    end--;
            }else if(nums[start] + nums[end] + nums[i] > 0){
                end--;
            }else
                start++;
        }
    }
    return result;
}
```