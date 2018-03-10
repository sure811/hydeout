---
layout: post
title: LeetCode - Different Ways to Add Parentheses
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Divide and Conquer
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.
<!--more-->

**Example 1**
Input: "2-1-1".
```
((2-1)-1) = 0
(2-(1-1)) = 2
```
Output: `[0, 2]`


**Example 2**
Input: "2*3-4*5"
```
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```
Output: `[-34, -14, -10, -10, 10]`
### Java Solution
```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < input.length(); i++) {
            if (isOperator(input.charAt(i))) {
                char operator = input.charAt(i);
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1));
                for (int num1 : left) {
                    for (int num2 : right) {
                        result.add(calculate(num1, num2, operator));
                    }
                }
            }
        }
        if (result.size() == 0) {
            result.add(Integer.valueOf(input));
        }
        return result;
    }
    public int calculate(int num1, int num2, char operator) {
        int result = 0;
        switch(operator) {
            case '+' : result = num1 + num2;
            break;

            case '-' : result = num1 - num2;
            break;

            case '*' : result = num1 * num2;
            break;
        }
        return result;
    }
    public boolean isOperator(char c) {
        if (c == '+' || c == '-' || c == '*')
            return true;
        return false;
    }
}
```