---
layout: post
title: LeetCode - Partition to K Equal Sum Subsets
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers nums and a positive integer k, find whether it's possible to divide this array into k non-empty subsets whose sums are all equal.
<!--more-->

**Example 1:**
```
Input: nums = [4, 3, 2, 3, 5, 2, 1], k = 4
Output: True
Explanation: It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```
**Note:**
* 1 <= k <= len(nums) <= 16.
* 0 < `nums[i]` < 10000.
### Java Solution
```java
class Solution {
    public boolean canPartitionKSubsets(int[] nums, int k) {
        Arrays.sort(nums);
        int sum = 0;
        for(int num : nums)
            sum += num;
        if(sum % k != 0) return false;
        boolean[] visited = new boolean[nums.length];
        for(int i = 0; i < k - 1; i++){
            if(!dfs(nums, sum / k, nums.length - 1, visited))
                return false;
        }
        return true;
    }

    private boolean dfs(int[] nums, int target, int start, boolean[] visited){
        if(target == 0) return true;
        if(target < 0) return false;

        for(int i = start; i >= 0; i--){
            if(!visited[i] && nums[i] <= target){
                visited[i] = true;
                if(dfs(nums, target - nums[i], i - 1, visited))
                    return true;
                else
                    visited[i] = false;
            }
        }
        return false;
    }
}
```