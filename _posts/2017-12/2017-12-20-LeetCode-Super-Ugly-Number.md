---
layout: post
title: LeetCode - Super Ugly Number
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, `[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32]` is the sequence of the first 12 super ugly numbers given primes = `[2, 7, 13, 19]` of size 4.
<!--more-->
Note:
(1) 1 is a super ugly number for any given primes.
(2) The given numbers in primes are in ascending order.
(3) 0 < k ≤ 100, 0 < n ≤ 106, 0 < primes`[i]` < 1000.
(4) The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

### Java Solution
```java
public int nthSuperUglyNumber(int n, int[] primes) {
    int size = primes.length;
    int q[] = new int[n];
    int idxes[] = new int[size];
    int vals[] = new int[size];
    q[0] = 1;
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < size; j++) {
            vals[j] = q[idxes[j]] * primes[j];
        }
        q[i] = findMin(vals);
        for (int j = 0; j < size; j++) {
            if (vals[j] == q[i]) {
                idxes[j] += 1;
            }
        }
    }
    return q[n - 1];
}

public int findMin(int[] nums) {
    int min = nums[0];
    for (int i = 1; i < nums.length; i++) {
        min = Math.min(min, nums[i]);
    }
    return min;
}
```