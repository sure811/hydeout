---
layout: post
title: [LeetCode] Task Scheduler
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
---

### Question Definition

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

**Example 1:**

<div>
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
</div>

**Note:**
The number of tasks is in the range `[1, 10000]`.
The integer n is in the range `[0, 100]`.

### Java Solution
```java
    public int leastInterval(char[] tasks, int n) {
        if (tasks == null || n < 0)
            return 0;

        if (n == 0)
            return tasks.length; // If there is no intervals, just execute all tasks one by one.

        int[] count = new int[26];

        int maxCount = 0;
        for (char task : tasks) {
            count[task - 'A']++;
            if (count[task - 'A'] > maxCount)
                maxCount = count[task - 'A'];
        }
        int sameMaxCount = 0;
        for (int cnt : count) {
            if (cnt == maxCount)
                sameMaxCount++;
        }
        return Math.max(tasks.length, (maxCount - 1) * (n + 1) + sameMaxCount);
    }
```
