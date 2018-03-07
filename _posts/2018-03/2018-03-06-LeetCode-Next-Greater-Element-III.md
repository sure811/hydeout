---
layout: post
title: LeetCode - Next Greater Element III
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a positive 32-bit integer n, you need to find the smallest 32-bit integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive 32-bit integer exists, you need to return -1.
<!--more-->
**Example 1:**
```
Input: 12
Output: 21
```

**Example 2:**
```
Input: 21
Output: -1
```
### Java Solution
```java
public int nextGreaterElement(int n) {
    char[] chars = Integer.toString(n).toCharArray();
    int index = chars.length - 2;
    while(index >= 0 && chars[index] >= chars[index + 1]) index--;
    if(index == -1) return -1;
    int index2 = chars.length - 1;
    while(index2 > index && chars[index] >= chars[index2]) index2--;
    char temp = chars[index];
    chars[index] = chars[index2];
    chars[index2] = temp;
    for(int i = index + 1, j = chars.length - 1; i < j; i++, j--){
        char temp2 = chars[i];
        chars[i] = chars[j];
        chars[j] = temp2;
    }
    double result = Double.parseDouble(new String(chars));
    return result >= Integer.MAX_VALUE ? -1 : (int)result;
}
```