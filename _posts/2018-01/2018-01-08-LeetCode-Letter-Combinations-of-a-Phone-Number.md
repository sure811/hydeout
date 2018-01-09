---
layout: post
title: LeetCode - Letter Combinations of a Phone Number
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a digit string, return all possible letter combinations that the number could represent.
<!--more-->
A mapping of digit to letters (just like on the telephone buttons) is given below.
```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
**Note:**

Although the above answer is in lexicographical order, your answer could be in any order you want.
### Java Solution
```java
class Solution {
    String[] phone = new String[]{"","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    public List<String> letterCombinations(String digits) {
        return letterCombinationsHelper(digits, 0);
    }

    private List<String> letterCombinationsHelper(String digits, int start) {
        List<String> result = new LinkedList<>();
        if(start == digits.length()) return result;

        String numbers = phone[digits.charAt(start) - '1'];
        for(char c: numbers.toCharArray()){
            List<String> temp = letterCombinationsHelper(digits, start + 1);
            if(temp.size() == 0)
                result.add(Character.toString(c));
            else
                for(String s : temp)
                    result.add(c + s);
        }
        return result;
    }
}
```