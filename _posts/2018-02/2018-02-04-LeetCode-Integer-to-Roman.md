---
layout: post
title: LeetCode - Integer to Roman
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an integer, convert it to a roman numeral.
<!--more-->

Input is guaranteed to be within the range from 1 to 3999.
### Java Solution
```java
public String intToRoman(int num) {
    String res = "";
    char roman[] = {'M', 'D', 'C', 'L', 'X', 'V', 'I'};
    int value[] = {1000, 500, 100, 50, 10, 5, 1};

    for (int n = 0; n < 7; n += 2) {
        int x = num / value[n];
        if (x < 4) {
            for (int i = 1; i <= x; ++i) res += roman[n];
        } else if (x == 4) res = res + roman[n] + roman[n - 1];
        else if (x > 4 && x < 9) {
            res += roman[n - 1];
            for (int i = 6; i <= x; ++i) res += roman[n];
        }
        else if (x == 9) res = res + roman[n] + roman[n - 2];
        num %= value[n];
    }
    return res;
}
```