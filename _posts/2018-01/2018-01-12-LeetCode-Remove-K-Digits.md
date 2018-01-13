---
layout: post
title: LeetCode - Remove K Digits
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.
<!--more-->

**Note:**
* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.

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
    if(k >= num.length()) return "0";
    Deque<Integer> res = new ArrayDeque<>();
    int n = num.length(), keep = n - k;
    for (char c : num.toCharArray()) {
        while (k > 0 && !res.isEmpty() && res.peek() > c - '0') {
            res.poll();
            --k;
        }
        res.push(c - '0');
    }
    String result = "";
    while(!res.isEmpty())
        //System.out.println(res.poll());
        result = res.poll() + result;
    int i = 0;
    for(; i < result.length() - 1 && result.charAt(i) == '0'; i++);

    return result.substring(i, Math.min(i + keep, result.length()));
}
```