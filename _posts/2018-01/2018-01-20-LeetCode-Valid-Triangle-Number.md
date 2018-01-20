---
layout: post
title: LeetCode - Valid Triangle Number
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.
**Example 1:**
```
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are:
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```
**Note:**
1. The length of the given array won't exceed 1000.
2. The integers in the given array are in the range of `[0, 1000]`.
### My Java Solution
```java
public int triangleNumber(int[] nums) {
    Arrays.sort(nums);
    int result = 0;
    for(int i = 0; i < nums.length; i++){
        for(int j = i + 1; j < nums.length; j++){
            for(int k = j + 1; k < nums.length; k++){
                if(nums[i] + nums[j] > nums[k])
                    result++;
            }
        }
    }
    return result;
}
```
### Best Java Solution
```java
public int triangleNumber(int[] nums) {
    int res = 0, n = nums.length;
    Arrays.sort(nums);
    for (int i = n - 1; i >= 2; --i) {
        int left = 0, right = i - 1;
        while (left < right) {
            if (nums[left] + nums[right] > nums[i]) {
                res += right - left;
                --right;
            } else {
                ++left;
            }
        }
    }
    return res;
}
```