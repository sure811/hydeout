---
layout: post
title: LeetCode - 2 Keys Keyboard
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
### Java Solution
```java
public int minSteps(int n) {
    if (n == 1) return 0;
    int res = n;
    for (int i = n - 1; i > 1; --i) {
        if (n % i == 0) {
            res = Math.min(res, minSteps(n / i) + i);
        }
    }
    return res;
}
```