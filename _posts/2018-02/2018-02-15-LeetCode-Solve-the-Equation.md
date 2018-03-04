---
layout: post
title: LeetCode - Solve the Equation
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Solve a given equation and return the value of x in the form of string "x=#value". The equation contains only '+', '-' operation, the variable x and its coefficient.

If there is no solution for the equation, return "No solution".

If there are infinite solutions for the equation, return "Infinite solutions".

If there is exactly one solution for the equation, we ensure that the value of x is an integer.
<!--more-->

Example 1:
```
Input: "x+5-3+x=6+x-2"
Output: "x=2"
```
Example 2:
```
Input: "x=x"
Output: "Infinite solutions"
```
Example 3:
```
Input: "2x=x"
Output: "x=0"
```
Example 4:
```
Input: "2x+3x-6x=x+2"
Output: "x=-1"
```
Example 5:
```
Input: "x=x+2"
Output: "No solution"
```
### Java Solution
```java
public String solveEquation(String equation) {
    int x = 0;
    int y = 0;
    equation = equation.replace("-", "+-");
    String[] equations1 = equation.split("=")[0].split("\\+");
    String[] equations2 = equation.split("=")[1].split("\\+");
    for(String equ : equations1){
        if(equ.length() == 0) continue;
        if(equ.contains("x")){
            if(equ.equals("x")) x++;
            else if(equ.equals("-x")) x--;
            else
                x += Integer.parseInt(equ.substring(0, equ.length() - 1));
        }else{
            y += Integer.parseInt(equ);
        }
    }
    for(String equ : equations2){
        if(equ.length() == 0) continue;
        if(equ.contains("x")){
            if(equ.equals("x")) x--;
            else if(equ.equals("-x")) x++;
            else
                x -= Integer.parseInt(equ.substring(0, equ.length() - 1));
        }else{
            y -= Integer.parseInt(equ);
        }
    }
    if(x == 0 && y == 0) return "Infinite solutions";
    if(x == 0) return "No solution";
    return "x=" + (- y / x);
}
```