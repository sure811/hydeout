---
layout: post
title: LeetCode - Maximum Swap
categories:
    - LeetCode
tags:
    - LeetCode
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

**Example 1:**

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
    char[] digits = Integer.toString(num).toCharArray();

    int[] buckets = new int[10];
    for (int i = 0; i < digits.length; i++) {
        buckets[digits[i] - '0'] = i;
    }

    for (int i = 0; i < digits.length; i++) {
        for (int k = 9; k > digits[i] - '0'; k--) {
            if (buckets[k] > i) {
                char tmp = digits[i];
                digits[i] = digits[buckets[k]];
                digits[buckets[k]] = tmp;
                return Integer.valueOf(new String(digits));
            }
        }
    }

    return num;
}
```
