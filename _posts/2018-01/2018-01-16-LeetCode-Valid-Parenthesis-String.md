---
layout: post
title: LeetCode - Valid Parenthesis String
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules:

1. Any left parenthesis '(' must have a corresponding right parenthesis ')'.
2. Any right parenthesis ')' must have a corresponding left parenthesis '('.
3. Left parenthesis '(' must go before the corresponding right parenthesis ')'.
4. '*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.
5. An empty string is also valid.
**Example 1:**
```
Input: "()"
Output: True
```
**Example 2:**
```
Input: "(*)"
Output: True
```
**Example 3:**
```
Input: "(*))"
Output: True
```
**Note:**
1. The string size will be in the range `[1, 100]`.
### Java Solution
```java
public boolean checkValidString(String s) {
    Deque<Integer> left = new ArrayDeque<>();
    Deque<Integer> star = new ArrayDeque<>();

    for(int i = 0; i < s.length(); i++){
        char c = s.charAt(i);
        if(c == '*') star.push(i);
        else if(c == '(') left.push(i);
        else {
            if(left.isEmpty() && star.isEmpty()) return false;
            if(!left.isEmpty())
                left.poll();
            else
                star.poll();
        }
    }
    if(left.size() > star.size()) return false;
    while(!left.isEmpty()){
        if(left.poll() > star.poll()) return false;
    }
    return true;
}
```