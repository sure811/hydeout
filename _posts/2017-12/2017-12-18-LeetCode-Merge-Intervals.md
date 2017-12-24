---
layout: post
title: LeetCode - Merge Intervals
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given a collection of intervals, merge all overlapping intervals.
<!--more-->

For example,
Given `[1,3],[2,6],[8,10],[15,18]`,
return `[1,6],[8,10],[15,18]`.

### Java Solution
```java
public List<Interval> merge(List<Interval> intervals) {
    if(intervals.size() < 2)
        return intervals;
    intervals.sort((o1, o2) -> o1.start == o2.start ? o1.end - o2.end: o1.start - o2.start);
    List<Interval> result = new LinkedList<>();
    int currentStart = intervals.get(0).start;
    int currentEnd = intervals.get(0).end;
    for(int i = 1; i < intervals.size(); i++){
        if(intervals.get(i).start > currentEnd){
            result.add(new Interval(currentStart, currentEnd));
            currentStart = intervals.get(i).start;
            currentEnd = intervals.get(i).end;
        }else{
            currentEnd = Math.max(currentEnd, intervals.get(i).end);
        }
    }
    result.add(new Interval(currentStart, currentEnd));
    return result;
}
```
