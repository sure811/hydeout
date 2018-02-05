---
layout: post
title: LeetCode - Complex Number Multiplication
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two strings representing two complex numbers.

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.
<!--more-->
**Example 1:**
```
Input: "1+1i", "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```
**Example 2:**
```
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```
**Note:**

1. The input strings will not have extra blank.
2. The input strings will be given in the form of a+bi, where the integer a and b will both belong to the range of `[-100, 100]`. And the output should be also in this form.
### Java Solution
```java
public String complexNumberMultiply(String a, String b) {
    int a1 = Integer.parseInt(a.substring(0, a.indexOf("+")));
    int a2 = Integer.parseInt(a.substring(a.indexOf("+") + 1, a.length() - 1));
    int b1 = Integer.parseInt(b.substring(0, b.indexOf("+")));
    int b2 = Integer.parseInt(b.substring(b.indexOf("+") + 1, b.length() - 1));
    return (a1 * b1 - a2 * b2) + "+" + (a1 * b2 + a2 * b1) + "i";
}
```