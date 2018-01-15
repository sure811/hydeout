---
layout: post
title: LeetCode - Binary Number with Alternating Bits
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.
<!--more-->

**Example 1:**
```
Input: 5
Output: True
Explanation:
The binary representation of 5 is: 101
```
**Example 2:**
```
Input: 7
Output: False
Explanation:
The binary representation of 7 is: 111.
```
**Example 3:**
```
Input: 11
Output: False
Explanation:
The binary representation of 11 is: 1011.
```
**Example 4:**
```
Input: 10
Output: True
Explanation:
The binary representation of 10 is: 1010.
```
### Java Solution
```java
public boolean hasAlternatingBits(int n) {
    int pre = n % 2;
    n = n / 2;
    while(n > 0){
        if(pre == n % 2)
            return false;
        pre = n % 2;
        n = n / 2;
    }
    return true;
}
```