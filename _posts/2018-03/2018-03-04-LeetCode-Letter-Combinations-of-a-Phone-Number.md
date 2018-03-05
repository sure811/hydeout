---
layout: post
title: LeetCode - Letter Combinations of a Phone Number
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.
<!--more-->
```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
**Note:**
Although the above answer is in lexicographical order, your answer could be in any order you want.
### Java Solution
```java
public List<String> letterCombinations(String digits) {
    String[] nums = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    List<String> result = new LinkedList<>();
    for(char c : digits.toCharArray()){
        List<String> temp = new LinkedList<>();
        for(char s : nums[c - '0'].toCharArray()){
            if(result.isEmpty())
                temp.add("" + s);
            else
                for(String res : result)
                    temp.add(res + s);
        }
        result = temp;
    }
    return result;
}
```