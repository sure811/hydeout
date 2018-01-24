---
layout: post
title: LeetCode - Summary Ranges
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a sorted integer array without duplicates, return the summary of its ranges.
<!--more-->

Example 1:
```
Input: [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
```
Example 2:
```
Input: [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
```
### Java Solution
```java
public List<String> summaryRanges(int[] nums) {
    int index = 1;
    List<String> result = new LinkedList<>();
    for(int i = 1; i < nums.length; i++){
        if(nums[i] == nums[i - 1] + 1)
            index++;
        else{
            if(index == 1){
                result.add(Integer.toString(nums[i - 1]));
            } else {
                result.add(nums[i - index] + "->" + nums[i - 1]);
            }
            index = 1;
        }
    }
    if(nums.length > 0){
        if(index == 1){
            result.add(Integer.toString(nums[nums.length - 1]));
        } else {
            result.add(nums[nums.length - index] + "->" + nums[nums.length - 1]);
        }}
    return result;
}
```