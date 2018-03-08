---
layout: post
title: LeetCode - Simplify Path
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an absolute path for a file (Unix-style), simplify it.
<!--more-->
For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
### Java Solution
```java
public String simplifyPath(String path) {
    Deque<String> deque = new ArrayDeque<>();
    String[] paths = path.split("/");
    for(String p : paths){
        if(p.isEmpty() || p.equals(".")) continue;
        if(p.equals("..")){
            if(!deque.isEmpty())
                deque.pop();
        }else deque.push(p);
    }
    StringBuilder result = new StringBuilder();
    while(!deque.isEmpty()){
        result.insert(0, "/" + deque.pop());
    }
    return result.length() == 0 ? "/" : result.toString();
}
```