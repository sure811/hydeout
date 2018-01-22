---
layout: post
title: LeetCode - Remove Duplicates from Sorted Array II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Follow up for "Remove Duplicates":
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = `[1,1,1,2,2,3]`,

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
### My Java Solution
```java
public int removeDuplicates(int[] nums) {
    int dupilicates = 0;
    for(int i = 2; i < nums.length; i++){
        if(nums[i] == nums[i - 1 - dupilicates] && nums[i] == nums[i - 2 - dupilicates]){
            dupilicates++;
        }
        else if(dupilicates > 0){
            nums[i - dupilicates] = nums[i];
        }
    }
    return nums.length - dupilicates;
}
```