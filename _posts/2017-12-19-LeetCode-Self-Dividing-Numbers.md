---
layout: post
title: LeetCode - Self Dividing Numbers
categories:
    - LeetCode
tags:
    - LeetCode
    - Easy
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

A self-dividing number is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.
<!--more-->

Example 1:
Input:
left = 1, right = 22
Output: `[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]`
Note:

The boundaries of each input argument are 1 <= left <= right <= 10000.

### Java Solution
```java
public List<Integer> selfDividingNumbers(int left, int right) {
    List<Integer> result = new LinkedList<>();
    for(int i = left; i <= right; i++){
        if(i % 10 == 0)
            continue;
        if(i < 10){
            result.add(i);
            continue;
        }
        boolean divided = true;
        int num = i;
        while(num > 0){
            if(num % 10 == 0 || i % (num % 10) != 0){
                divided = false;
                break;
            }
            num = num / 10;
        }
        if(divided)
            result.add(i);
    }
    return result;
}
```