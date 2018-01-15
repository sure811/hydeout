---
layout: post
title: LeetCode - Monotone Increasing Digits
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Greedy
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a non-negative integer N, find the largest number that is less than or equal to N with monotone increasing digits.

(Recall that an integer has monotone increasing digits if and only if each pair of adjacent digits x and y satisfy x <= y.)

**Example 1:**
```
Input: N = 10
Output: 9
```
**Example 2:**
```
Input: N = 1234
Output: 1234
```
**Example 3:**
```
Input: N = 332
Output: 299
```
**Note:** N is an integer in the range `[0, 10^9]`.
### Java Solution
```java
public int monotoneIncreasingDigits(int N) {
    if(N < 10) return N;
    String s = Integer.toString(N);
    StringBuilder result = new StringBuilder();
    int i = 1;
    for(; i < s.length(); i++){
        if(s.charAt(i) < s.charAt(i - 1)){
            break;
        }
        result.append(s.charAt(i - 1));
    }
    if(i == s.length()) return N;
    i--;
    while(i >= 1 && s.charAt(i - 1) == s.charAt(i)) {
        i--;
        result.deleteCharAt(result.length() - 1);
    }
    if(s.charAt(i) != '0')
        result.append(s.charAt(i) - '0' - 1);
    for(int j = i + 1; j < s.length(); j++)
        result.append('9');
    return Integer.parseInt(result.toString());
}
```