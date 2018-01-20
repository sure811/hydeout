---
layout: post
title: LeetCode - Task Scheduler
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.
<!--more-->

**Example 1:**
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```
**Note:**
1. The number of tasks is in the range `[1, 10000]`.
2. The integer n is in the range `[0, 100]`.
### Java Solution
```java
public int leastInterval(char[] tasks, int n) {
    int mx = 0, mxCnt = 0;
    int[] cnt = new int[26];
    for (char task : tasks) {
        ++cnt[task - 'A'];
        if (mx == cnt[task - 'A']) {
            ++mxCnt;
        } else if (mx < cnt[task - 'A']) {
            mx = cnt[task - 'A'];
            mxCnt = 1;
        }
    }
    int partCnt = mx - 1;
    int partLen = n - (mxCnt - 1);
    int emptySlots = partCnt * partLen;
    int taskLeft = tasks.length - mx * mxCnt;
    int idles = Math.max(0, emptySlots - taskLeft);
    return tasks.length + idles;
}
```