---
layout: post
title: LeetCode - Mini Parser
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a nested list of integers represented as a string, implement a parser to deserialize it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.
<!--more-->

**Note:** You may assume that the string is well-formed:

* String is non-empty.
* String does not contain white spaces.
* String contains only digits 0-9, `[, - ,, ]`.

**Example 1:**
```
Given s = "324",

You should return a NestedInteger object which contains a single integer 324.
```
**Example 2:**
```
Given s = "[123,[456,[789]]]",

Return a NestedInteger object containing a nested list with 2 elements:

1. An integer containing value 123.
2. A nested list containing two elements:
    i.  An integer containing value 456.
    ii. A nested list with one element:
         a. An integer containing value 789.
```
### Java Solution
```java
public NestedInteger deserialize(String s) {
    if(s.indexOf("[") < 0) return new NestedInteger(Integer.parseInt(s));

    Deque<NestedInteger> deque = new ArrayDeque<>();
    NestedInteger cur = null;
    int num = 0;
    boolean positive = false;
    for(int i = 0; i < s.length(); i++){
        char c = s.charAt(i);
        if(c == '['){
            if(cur != null)
                deque.push(cur);
            cur = new NestedInteger();
        } else if(c == ']'){
            if(s.charAt(i - 1) >= '0' && s.charAt(i - 1) <= '9'){
                if(positive)
                    num = -num;
                cur.add(new NestedInteger(num));
            }
            NestedInteger parent = deque.poll();
            if(parent == null)
                return cur;
            parent.add(cur);
            cur = parent;
            num = 0;
            positive = false;
        } else if(c == ','){
            if(s.charAt(i - 1) >= '0' && s.charAt(i - 1) <= '9'){
                if(positive)
                    num = -num;
                cur.add(new NestedInteger(num));
            }
            num = 0;
            positive = false;
        } else {
            if(c == '-')
                positive = true;
            else
                num = num * 10 + (c - '0');
        }
    }
    return cur;
}
```