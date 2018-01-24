---
layout: post
title: LeetCode - 4Sum
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
<!--more-->

Note: The solution set must not contain duplicate quadruplets.

For example, given array S = `[1, 0, -1, 0, -2, 2]`, and target = 0.
```
A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```
### Java Solution
```java
public List<List<Integer>> fourSum(int[] nums, int target) {
    Arrays.sort(nums);

    List<List<Integer>> result = new LinkedList<>();
    for(int j = 0; j < nums.length - 3; j++){
        if (j > 0 && nums[j] == nums[j - 1]) continue;
        for(int i = j + 1; i < nums.length - 2; i++){
            if (i > j + 1 && nums[i] == nums[i - 1]) continue;
            int left = i + 1, right = nums.length - 1;
            while(left < right){
                if(nums[i] + nums[j] + nums[left] + nums[right] == target){
                    List<Integer> cur = new LinkedList<>();
                    cur.add(nums[j]);
                    cur.add(nums[i]);
                    cur.add(nums[left]);
                    cur.add(nums[right]);
                    result.add(cur);
                    while (left < right && nums[left] == nums[left + 1]) ++left;
                    while (left < right && nums[right] == nums[right - 1]) --right;
                    left++;
                    right--;
                }else if(nums[i] + nums[j] + nums[left] + nums[right] < target)
                    left++;
                else
                    right--;
            }
        }
    }
    return result;
}
```