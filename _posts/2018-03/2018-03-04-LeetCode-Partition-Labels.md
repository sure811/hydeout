---
layout: post
title: LeetCode - Partition Labels
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Two Pointers
    - Greedy
excerpt_separator: "<!--more-->"
---

### Question Definition
A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.
<!--more-->

**Example 1:**
```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```
**Note:**

1. S will have length in range `[1, 500]`.
2. S will consist of lowercase letters ('a' to 'z') only.
### Java Solution
```java
public List<Integer> partitionLabels(String S) {
    int[] ends = new int[26];

    for(int i = S.length() - 1; i >= 0; i--){
        if(ends[S.charAt(i) - 'a'] == 0)
            ends[S.charAt(i) - 'a'] = i;
    }
    int start = 0;
    int end = ends[S.charAt(0) - 'a'];
    List<Integer> result = new LinkedList<>();
    for(int i = 1; i < S.length(); i++){
        if(i <= end){
            if(ends[S.charAt(i) - 'a'] > end)
                end = ends[S.charAt(i) - 'a'];
        }else{
            if(ends[S.charAt(i) - 'a'] > end){
                result.add(end - start + 1);
                start = i;
                end = ends[S.charAt(i) - 'a'];
            }
        }
    }
    result.add(end - start + 1);
    return result;
}
```