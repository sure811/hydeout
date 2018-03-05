---
layout: post
title: LeetCode - Minimum Time Difference
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of 24-hour clock time points in "Hour:Minutes" format, find the minimum minutes difference between any two time points in the list.
<!--more-->
**Example 1:**
```
Input: ["23:59","00:00"]
Output: 1
```
**Note:**
1. The number of time points in the given list is at least 2 and won't exceed 20000.
2. The input time is legal and ranges from 00:00 to 23:59.
### Java Solution
```java
public int findMinDifference(List<String> timePoints) {
    int dis = Integer.MAX_VALUE;
    for(int i = 0; i < timePoints.size(); i++)
        for(int j = i + 1; j < timePoints.size(); j++){
            int x = Integer.parseInt(timePoints.get(i).substring(0,2)) * 60 + Integer.parseInt(timePoints.get(i).substring(3));
            int y = Integer.parseInt(timePoints.get(j).substring(0,2)) * 60 + Integer.parseInt(timePoints.get(j).substring(3));

            dis =  Math.min(dis, Math.min(Math.abs(x - y), Math.min(Math.abs(x - y + 24 * 60), Math.abs(x - y - 24 * 60))));
            if(dis == 0) return 0;
    }
    return dis;
}
```