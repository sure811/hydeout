---
layout: post
title: LeetCode - Palindrome Partitioning
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.
<!--more-->

For example, given s = "aab",
Return
```
[
  ["aa","b"],
  ["a","a","b"]
]
```
### Java Solution
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new LinkedList<>();
        List<String> cur = new LinkedList<>();
        partitionHelper(s, 0, cur, result);
        return result;
    }

    private void partitionHelper(String s, int start, List<String> cur, List<List<String>> result){
        if(start == s.length()){
            result.add(new LinkedList<>(cur));
            return;
        }
        for(int i = start; i < s.length(); i++){
            if(isPalindrome(s, start, i)){
                cur.add(s.substring(start, i + 1));
                partitionHelper(s, i + 1, cur, result);
                cur.remove(cur.size() - 1);
            }
        }
    }

    private boolean isPalindrome(String s, int start, int end){
        while(start < end){
            if(s.charAt(start) != s.charAt(end))
                return false;
            start++;
            end--;
        }
        return true;
    }
}
```