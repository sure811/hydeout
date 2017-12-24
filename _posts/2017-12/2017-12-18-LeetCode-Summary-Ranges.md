---
layout: post
title: LeetCode - Summary Ranges
categories:
    - LeetCode
tags:
    - LeetCode
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
    List<String> result = new LinkedList<>();
    if(nums.length == 0)
        return result;
    int start = nums[0];
    int end = nums[0];
    for(int i = 1; i < nums.length; i++){
        if(nums[i] == end + 1)
            end = nums[i];
        else{
            if(start == end)
                result.add("" + start);
            else{
                result.add(start + "->" + end);
            }
            start = nums[i];
            end = nums[i];
        }
    }
    if(start == end)
        result.add("" + start);
    else{
        result.add(start + "->" + end);
    }
    return result;
}
```
