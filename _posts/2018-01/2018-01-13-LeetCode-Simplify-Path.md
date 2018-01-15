---
layout: post
title: LeetCode - Simplify Path
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Stack
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
    String[] dirs = path.split("/");

    Deque<String> deque = new ArrayDeque<>();

    for(String dir : dirs){
        if(dir.equals(".") || dir.isEmpty()) continue;
        if(dir.equals("..")){
            deque.poll();
        }else
            deque.push(dir);
    }
    String result = "";
    while(!deque.isEmpty()){
        if(result.isEmpty())
            result = deque.poll();
        else
            result = deque.poll() + "/" + result;
    }
    return "/" + result;
}
```