---
layout: post
title: LeetCode - Merge Intervals
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
### My Java Solution
```java
public List<Interval> merge(List<Interval> intervals) {
    Map<Integer, Integer> map = new TreeMap<>();
    for(Interval interval : intervals){
        if(map.containsKey(interval.start))
            map.put(interval.start, Math.max(interval.end, map.get(interval.start)));
        else
            map.put(interval.start, interval.end);
    }
    int preStart = -1, preEnd = -1;
    List<Interval> result = new LinkedList<>();
    for(Map.Entry<Integer, Integer> entry : map.entrySet()){
        if(preStart == -1){
            preStart = entry.getKey();
            preEnd = entry.getValue();
        }else{
            if(entry.getKey() <= preEnd){
                preStart = Math.min(preStart, entry.getKey());
                preEnd = Math.max(preEnd, entry.getValue());
            }else{
                result.add(new Interval(preStart, preEnd));
                preStart = entry.getKey();
                preEnd = entry.getValue();
            }
        }
    }
    if(preStart != -1){
        result.add(new Interval(preStart, preEnd));
    }
    return result;
}
```