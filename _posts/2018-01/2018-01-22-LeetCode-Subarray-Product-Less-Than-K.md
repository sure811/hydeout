---
layout: post
title: LeetCode - Subarray Product Less Than K
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Your are given an array of positive integers nums.

Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than k.
<!--more-->
**Example 1:**
```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```
**Note:**

* 0 < nums.length <= 50000.
* 0 < nums[i] < 1000.
* 0 <= k < 10^6.
### Java Solution
```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    int result = 0;
    int left = 0;
    int right = 0;
    int product = nums[0];
    while(left < nums.length){
        if(right < left){
            right = left;
            product = nums[left];
        }
        while(product < k && ++right < nums.length){
            product *= nums[right];
        }
        right = Math.min(right, nums.length);
        result += right - left;
        product = product / nums[left];
        left++;
    }
    return result;
}
```