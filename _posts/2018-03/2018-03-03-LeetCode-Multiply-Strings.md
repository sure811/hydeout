---
layout: post
title: LeetCode - Multiply Strings
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.
<!--more-->

**Note:**

1. The length of both num1 and num2 is < 110.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

### Java Solution
```java
public String multiply(String num1, String num2) {
    int[] result = new int[num1.length() + num2.length()];
    for(int i = 0; i < num1.length(); i++){
        for(int j = 0; j < num2.length(); j++){
            int x = num1.charAt(i) - '0';
            int y = num2.charAt(j) - '0';
            result[i + j + 1] += x * y;
            int temp = i + j + 1;
            while(result[temp] > 9){
                result[temp - 1] += result[temp] / 10;
                result[temp] = result[temp] % 10;
                temp --;
            }
        }
    }
    String resultStr = "";
    boolean notZero = true;
    for(int i : result){
        if(i == 0 && notZero) continue;
        notZero = false;
        resultStr += i;
    }

    return resultStr == "" ? "0" : resultStr;
}
```