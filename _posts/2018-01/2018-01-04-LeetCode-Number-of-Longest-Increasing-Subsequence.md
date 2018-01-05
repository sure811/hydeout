---
layout: post
title: LeetCode - Number of Longest Increasing Subsequence
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an unsorted array of integers, find the number of longest increasing subsequence.
<!--more-->

**Example 1:**
```
Input: [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequence are [1, 3, 4, 7] and [1, 3, 5, 7].
```
**Example 2:**
```
Input: [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```
**Note:** Length of the given array will be not exceed 2000 and the answer is guaranteed to be fit in 32-bit signed int.
### Java Solution
```java
public int findNumberOfLIS(int[] nums) {
    if(nums.length == 0) return 0;
    TreeMap<Integer, Integer[]> map = new TreeMap<>();
    for(int num : nums){
        Integer[] count = new Integer[]{1, 1};
        if(map.containsKey(num))
            count = map.get(num);
        int _max = 1;
        int _maxCount = 1;
        for(Map.Entry<Integer, Integer[]> entry : map.entrySet()){
            if(entry.getKey() >= num)
                break;
            if(_max < entry.getValue()[0]){
                _max = entry.getValue()[0];
                _maxCount = entry.getValue()[1];
            } else if(_max == entry.getValue()[0]){
                _maxCount += entry.getValue()[1];
            }
        }
        if(count[0] < _max + 1){
            count[0] = _max + 1;
            count[1] = _maxCount;
        } else if(count[0] == _max + 1){
            count[1] += _maxCount;
        }
        map.put(num, count);
    }
    int max = 0;
    int maxCount = 0;
    for(Map.Entry<Integer, Integer[]> entry : map.entrySet()){
        if(entry.getValue()[0] > max){
            max = entry.getValue()[0];
            maxCount = entry.getValue()[1];
        } else if(entry.getValue()[0] == max){
            maxCount += entry.getValue()[1];
        }
    }
    return maxCount;
}
```