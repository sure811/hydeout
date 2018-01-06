---
layout: post
title: LeetCode - Find Smallest Letter Greater Than Target
categories:
    - LeetCode
tags:
    - LeetCode
    - Easy
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = `['a', 'b']`, the answer is 'a'.
<!--more-->

Examples:
```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```
Note:
1. letters has a length in range `[2, 10000]`.
2. letters consists of lowercase letters, and contains at least 2 unique letters.
3. target is a lowercase letter.
### Java Solution
```java
public char nextGreatestLetter(char[] letters, char target) {
    int start = 0;
    int end = letters.length - 1;
    while(start <= end){
        int mid = (start + end) / 2;
        if(letters[mid] == target){
            while(++mid < letters.length && letters[mid] == target);
            return letters[mid % letters.length];
        }
        if(letters[mid] < target)
            start = mid + 1;
        else
            end = mid - 1;
    }
    return letters[start % letters.length];
}
```