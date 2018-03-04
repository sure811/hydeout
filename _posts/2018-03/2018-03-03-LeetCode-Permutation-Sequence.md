---
layout: post
title: LeetCode - Permutation Sequence
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
The set `[1,2,3,…,n]` contains a total of n! unique permutations.
<!--more-->

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

Given n and k, return the kth permutation sequence.

**Note: ** Given n will be between 1 and 9 inclusive.
### Java Solution
```java
public String getPermutation(int n, int k) {
    String res = "";
    StringBuilder num = new StringBuilder("123456789");
    int[] f = new int[n];
    f[0] = 1;
    for (int i = 1; i < n; ++i) f[i] = f[i - 1] * i;
    --k;
    for (int i = n; i >= 1; --i) {
        int j = k / f[i - 1];
        k %= f[i - 1];
        res += num.charAt(j);
        num.deleteCharAt(j);
    }
    return res;
}
```