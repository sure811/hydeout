---
layout: post
title: LeetCode - H-Index II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Follow up for H-Index: What if the citations array is sorted in ascending order? Could you optimize your algorithm?
### Java Solution
```java
public int hIndex(int[] citations) {
    int len = citations.length, left = 0, right = len - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (citations[mid] == len - mid) return len - mid;
        else if (citations[mid] > len - mid) right = mid - 1;
        else left = mid + 1;
    }
    return len - left;
}
```