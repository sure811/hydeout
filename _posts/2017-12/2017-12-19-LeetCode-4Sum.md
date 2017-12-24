---
layout: post
title: LeetCode - 4Sum
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
<!--more-->

Note: The solution set must not contain duplicate quadruplets.

```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

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
    LinkedList<Integer> cur = new LinkedList<>();
    List<List<Integer>> result = new LinkedList<>();
    fourSumHelper(nums, cur, 4, target, 0, nums.length - 1, result);
    return result;
}

private void fourSumHelper(int[] nums, LinkedList<Integer> cur, int k, int target, int start, int end, List<List<Integer>> result){
    if(k <= 0)
        return;
    if(k == 1){
        for(int i = start; i <= end; i++){
            if(nums[i] == target){
                LinkedList<Integer> temp = new LinkedList<>(cur);
                temp.add(nums[i]);
                result.add(temp);
            }
        }
        return;
    }

    if(k == 2){
        twoSumHelper(nums, cur, k, target, start, end, result);
        return;
    }

    for(int i = start; i <= end - k + 1; i++) {
        if(i > start && nums[i] == nums[i-1]) continue;
        cur.addLast(nums[i]);
        fourSumHelper(nums, cur, k - 1, target - nums[i], i + 1, end, result);
        cur.removeLast();
    }

    return;
}

private void twoSumHelper(int[] nums, LinkedList<Integer> cur, int k, int target, int start, int end,  List<List<Integer>> result){
    while(start < end){
        int sum = nums[start] + nums[end];
        if(sum == target) {
            LinkedList<Integer> temp = new LinkedList<>(cur);
            temp.add(nums[start]);
            temp.add(nums[end]);
            result.add(temp);
            start++;
            end--;
            while(start < nums.length && nums[start] == nums[start-1]) start++;
            while(end >= 0 && nums[end] == nums[end+1]) end--;
        }
        else if(sum < target)
            start++;
        else
            end--;
    }
    return;
}
```