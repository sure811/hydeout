---
layout: post
title: LeetCode - Subarray Product Less Than K
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Two Points
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
* 0 < nums`[i]` < 1000.
* 0 <= k < 10^6.

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.


### Java Solution
```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    if (k < 2) {
        return 0;
    }
    int result = 0;
        int product = 1;
        for (int i = 0, right = 0; right < nums.length; right++) {
            product *= nums[right];
            while (i < nums.length && product >= k) {
                product /= nums[i++];
            }
            result += right - i + 1;
        }
        return result;
}
```
