---
layout: post
title: LeetCode -
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, +, -, *, / operators and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid.
<!--more-->

Some examples:
```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```
**Note: Do not use** the eval built-in library function.
### Java Solution
```java
public int calculate(String s) {
    int res = 0, d = 0;
    char sign = '+';
    Deque<Integer> nums = new ArrayDeque<>();
    for (int i = 0; i < s.length(); ++i) {
        if (s.charAt(i) >= '0') {
            d = d * 10 + (s.charAt(i) - '0');
        }
        if ((s.charAt(i) < '0' && s.charAt(i) != ' ') || i == s.length() - 1) {
            if (sign == '+') nums.push(d);
            if (sign == '-') nums.push(-d);
            if (sign == '*' || sign == '/') {
                int tmp = sign == '*' ? nums.peek() * d : nums.peek() / d;
                nums.poll();
                nums.push(tmp);
            }
            sign = s.charAt(i);
            d = 0;
        }
    }
    while (!nums.isEmpty()) {
        res += nums.poll();
    }
    return res;
}
```