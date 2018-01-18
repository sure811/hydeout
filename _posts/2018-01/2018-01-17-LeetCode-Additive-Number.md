---
layout: post
title: LeetCode - Additive Number
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Additive number is a string whose digits can form additive sequence.

A valid additive sequence should contain at least three numbers. Except for the first two numbers, each subsequent number in the sequence must be the sum of the preceding two.
<!--more-->

For example:
"112358" is an additive number because the digits can form an additive sequence: 1, 1, 2, 3, 5, 8.
```
1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8
```
"199100199" is also an additive number, the additive sequence is: 1, 99, 100, 199.
```
1 + 99 = 100, 99 + 100 = 199
```
**Note: **Numbers in the additive sequence cannot have leading zeros, so sequence 1, 2, 03 or 1, 02, 3 is invalid.

Given a string containing only digits '0'-'9', write a function to determine if it's an additive number.

**Follow up:**
How would you handle overflow for very large input integers?
### Java Solution
```java
class Solution {
    public boolean isAdditiveNumber(String num) {
        if(num.length() == 0) return true;
        if(num.length() < 3) return false;
        for(int i = 1; i < num.length(); i++){
            if(i > 1 && num.startsWith("0")) break;
            double x1 = Double.parseDouble(num.substring(0, i));
            if(isAdditiveNumber(num.substring(i), x1))
                return true;
        }
        return false;
    }

    public boolean isAdditiveNumber(String num, double x1) {
        for(int j = 1; j < num.length(); j++){
            if(j > 1 && num.startsWith("0")) break;
            double x2 = Double.parseDouble(num.substring(0, j));
            String next = String.format("%.0f", x1 + x2);
            if(num.startsWith(next, j) && (next.equals(num.substring(j)) || isAdditiveNumber(num.substring(j), x2))){
                return true;
            }
        }
        return false;
    }
}
```