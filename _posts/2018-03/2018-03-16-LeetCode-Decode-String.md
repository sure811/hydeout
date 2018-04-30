---
layout: post
title: LeetCode - Decode String
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Stack
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an encoded string, return it's decoded string.

The encoding rule is: `k[encoded_string]`, where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or `2[4]`.

Examples:
```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```
### Java Solution
```java
public String decodeString(String s) {
    Deque<String> strings = new ArrayDeque<>();
    Deque<Integer> nums = new ArrayDeque<>();
    String res = "", t = "";
    int cnt = 0;
    for (int i = 0; i < s.length(); ++i) {
        if (s.charAt(i) >= '0' && s.charAt(i) <= '9') {
            cnt = 10 * cnt + (int)(s.charAt(i) - '0');
        } else if (s.charAt(i) == '[') {
            nums.push(cnt);
            strings.push(t);
            cnt = 0;
            t = "";
        } else if (s.charAt(i) == ']') {
            int k = nums.poll();
            String top = strings.poll();
            for (int j = 0; j < k; ++j) top += t;
            t = top;
        } else {
            t += s.charAt(i);
        }
    }
    System.out.println(strings.size());
    return strings.isEmpty() ? t : strings.peek();
}
```