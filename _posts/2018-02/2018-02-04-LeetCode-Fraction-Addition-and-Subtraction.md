---
layout: post
title: LeetCode - Fraction Addition and Subtraction
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string representing an expression of fraction addition and subtraction, you need to return the calculation result in string format. The final result should be irreducible fraction. If your final result is an integer, say 2, you need to change it to the format of fraction that has denominator 1. So in this case, 2 should be converted to 2/1.
<!--more-->
**Example 1:**
```
Input:"-1/2+1/2"
Output: "0/1"
```
**Example 2:**
```
Input:"-1/2+1/2+1/3"
Output: "1/3"
```
**Example 3:**
```
Input:"1/3-1/2"
Output: "-1/6"
```
**Example 4:**
```
Input:"5/3+1/3"
Output: "2/1"
```
**Note:**
1. The input string only contains '0' to '9', '/', '+' and '-'. So does the output.
2. Each fraction (input and output) has format ±numerator/denominator. If the first input fraction or the output is positive, then '+' will be omitted.
3. The input only contains valid irreducible fractions, where the numerator and denominator of each fraction will always be in the range [1,10]. If the denominator is 1, it means this fraction is actually an integer in a fraction format defined above.
4. The number of given fractions will be in the range [1,10].
5. The numerator and denominator of the final result are guaranteed to be valid and in the range of 32-bit int.

### Java Solution
```java
class Solution {
    public String fractionAddition(String expression) {
        if (expression == null || expression.length() == 0) {
            return expression;
        }

        expression = expression.replace("-", "+-");
        String[] factors = expression.split("\\+");

        List<Integer> numerators = new ArrayList();
        List<Integer> denominators = new ArrayList();

        for (int i = 0; i < factors.length; i++) {
            if ("".equals(factors[i])) {
                continue;
            }
            String[] numbers = factors[i].split("/");
            numerators.add(Integer.valueOf(numbers[0]));
            denominators.add(Integer.valueOf(numbers[1]));
        }

        int denominator = 1;
        for (int value : denominators) {
            denominator *= value;
        }

        int numerator = 0;
        for (int i = 0; i < numerators.size(); i++) {
            numerator += numerators.get(i) * (denominator / denominators.get(i));
        }

        int gcd = GCD(Math.abs(numerator), Math.abs(denominator));
        if (gcd == 0) {
            return "-1";
        }

        if (numerator > 0 && denominator < 0) {
            numerator = -numerator;
            denominator = -denominator;
        }

        return numerator / gcd + "/" + denominator / gcd;
    }

    private int GCD(int numerator, int denominator) {
        if (denominator == 0) {
            return numerator;
        }
        return GCD(denominator, numerator % denominator);
    }
}
```