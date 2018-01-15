---
layout: post
title: LeetCode - Gas Station
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
There are N gas stations along a circular route, where the amount of gas at station i is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.
<!--more-->

**Note:**

The solution is guaranteed to be unique.
### Java Solution
```java
public int canCompleteCircuit(int[] gas, int[] cost) {
    int start = 0, netGasSum = 0, curGasSum = 0;
    for(int i=0; i<cost.length; i++) {
        netGasSum += gas[i] - cost[i];
        curGasSum += gas[i] - cost[i];
        if(curGasSum<0) {
            start = i+1;
            curGasSum = 0;
        }
    }
    if(netGasSum < 0) return -1;
    return start;
}
```