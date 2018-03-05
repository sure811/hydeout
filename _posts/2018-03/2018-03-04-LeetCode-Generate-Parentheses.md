---
layout: post
title: LeetCode - Generate Parentheses
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
<!--more-->
For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```
### Java Solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new LinkedList<>();
        String cur = "";
        generateParenthesis(n, 0, cur, result);
        return result;
    }

    private void generateParenthesis(int n, int t, String cur, List<String> result){
        if(n == 0){
            while(t-- > 0) cur += ")";
            result.add(cur);
            return;
        }
        generateParenthesis(n - 1, t + 1, cur + "(", result);
        if(t > 0)
            generateParenthesis(n, t - 1, cur + ")", result);
    }
}
```