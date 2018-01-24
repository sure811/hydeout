---
layout: post
title: LeetCode - 3Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
<!--more-->

Note: The solution set must not contain duplicate triplets.
```
For example, given array S = `[-1, 0, 1, 2, -1, -4],

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
    for(int i = 0; i < nums.length - 2; i++){
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1, right = nums.length - 1;
        while(left < right){
            if(nums[i] + nums[left] + nums[right] == 0){
                List<Integer> cur = new LinkedList<>();
                cur.add(nums[i]);
                cur.add(nums[left]);
                cur.add(nums[right]);
                result.add(cur);
                while (left < right && nums[left] == nums[left + 1]) ++left;
                while (left < right && nums[right] == nums[right - 1]) --right;
                left++;
                right--;
            }else if(nums[i] + nums[left] + nums[right] < 0)
                left++;
            else
                right--;
        }
    }
    return result;
}
```