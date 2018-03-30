---
layout: post
title: LeetCode - Increasing Subsequences
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .
<!--more-->

**Example:**
```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```
**Note:**
1. The length of the given array will not exceed 15.
2. The range of integer in the given array is `[-100,100]`.
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.
### Java Solution
```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        Set<List<Integer>> set = new HashSet<>();
        for(int i = 2; i <= nums.length; i++) {
            List<Integer> cur = new LinkedList<>();
            helper(nums, 0, i, cur, set);
        }
        return set.stream().collect(Collectors.toList());
    }

    private void helper(int[] nums, int start, int length, List<Integer> cur, Set<List<Integer>> set) {
        if(length == 0) {
            set.add(new LinkedList<>(cur));
            return;
        }

        for(int i = start; i < nums.length; i++){
            if(cur.size() == 0 || nums[i] >= cur.get(cur.size() - 1)){
                cur.add(nums[i]);
                helper(nums, i + 1, length - 1, cur, set);
                cur.remove(cur.size() - 1);
            }
        }
    }
}
```