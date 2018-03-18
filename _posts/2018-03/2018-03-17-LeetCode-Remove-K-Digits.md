---
layout: post
title: LeetCode - Remove K Digits
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**

* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.
<!--more-->
**Example 1:**
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```
**Example 2:**
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```
**Example 3:**
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```
### Java Solution
```java
public String removeKdigits(String num, int k) {
    int remain = num.length() - k;
    StringBuilder sb = new StringBuilder();
    for(char c : num.toCharArray()){
        while(sb.length() > 0 && k > 0 && sb.charAt(sb.length() - 1) > c){
            sb.deleteCharAt(sb.length() - 1);
            k--;
        }
        sb.append(c);
    }

    sb.delete(remain, sb.length());
    while (sb.length() > 0 && sb.charAt(0) == '0') sb.deleteCharAt(0);
    return sb.length() == 0 ? "0" : sb.toString();
}
```