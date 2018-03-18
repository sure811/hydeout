---
layout: post
title: LeetCode - Evaluate Reverse Polish Notation
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.
<!--more-->

Some examples:
```
  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6
```
### Java Solution
```java
public int evalRPN(String[] tokens) {
    Deque<Integer> stack = new ArrayDeque<>();
    for(String token : tokens) {
        if(token.equals("+")){
            stack.push(stack.pop() + stack.pop());
        } else if(token.equals("-")){
            int temp = stack.pop();
            stack.push(stack.pop() - temp);
        } else if(token.equals("*")){
            stack.push(stack.pop() * stack.pop());
        } else if(token.equals("/")){
            int temp = stack.pop();
            stack.push(stack.pop() / temp);
        } else
            stack.push(Integer.parseInt(token));
    }
    return stack.pop();
}
```