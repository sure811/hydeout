---
layout: post
title: LeetCode - Maximum Swap
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-negative integer, you could swap two digits at most once to get the maximum valued number. Return the maximum valued number you could get.
<!--more-->

**Example 1:**
```
Input: 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
```
**Example 2:**
```
Input: 9973
Output: 9973
Explanation: No swap.
```
**Note:**
1. The given number is in the range `[0, 108]`
### Java Solution
```java
public int maximumSwap(int num) {
    char[] numOri = Integer.toString(num).toCharArray();
    char[] nums = Integer.toString(num).toCharArray();
    Arrays.sort(nums);
    for(int i = 0; i < nums.length; i++){
        if(numOri[i] != nums[nums.length - 1 - i]){
            char max = nums[nums.length - 1 - i];
            for(int j = nums.length - 1; j > i; j--){
                if(numOri[j] == max){
                    numOri[j] = numOri[i];
                    numOri[i] = max;
                    return Integer.parseInt(new String(numOri));
                }
            }
        }
    }
    return num;
}
```