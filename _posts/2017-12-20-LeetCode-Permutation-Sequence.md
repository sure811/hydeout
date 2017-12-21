---
layout: post
title: LeetCode - Permutation Sequence
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
    - Permutation
excerpt_separator: "<!--more-->"
---

### Question Definition

The set `[1,2,3,…,n]` contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

### Java Solution
```java
public String getPermutation(int n, int k) {
    String res = "";
    int[] f = new int[n];
    f[0] = 1;
    List<String> nums = new LinkedList<>();
    for (int i = 1; i < n; ++i){
        f[i] = f[i - 1] * i;
        nums.add(Integer.toString(i));
    }
    nums.add(Integer.toString(n));
    --k;
    for (int i = n; i >= 1; --i) {
        int j = k / f[i - 1];
        k %= f[i - 1];
        res += nums.get(j);
        nums.remove(j);
    }
    return res;
}
```