---
layout: post
title: LeetCode - Delete Operation for Two Strings
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.
<!--more-->
**Example 1:**
```
Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```
**Note:**
1. The length of given words won't exceed 500.
2. Characters in given words can only be lower-case letters.
### Java Solution
```java
public int minDistance(String word1, String word2) {
    if(word1.isEmpty()) return word2.length();
    if(word2.isEmpty()) return word1.length();
    int[][] dp = new int[word1.length() + 1][word2.length() + 1];
    for(int i = 1; i <= word1.length(); i++){
        for(int j = 1; j <= word2.length(); j++){
            if(word1.charAt(i - 1) == word2.charAt(j - 1)){
                dp[i][j] = dp[i - 1][j - 1] + 1;
            }else{
                dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
            }
        }
    }
    return word1.length() + word2.length() - 2 * dp[word1.length()][word2.length()];
}
```