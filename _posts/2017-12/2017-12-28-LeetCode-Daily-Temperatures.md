---
layout: post
title: LeetCode - Daily Temperatures
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of daily temperatures, produce a list that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.
<!--more-->

For example, given the list temperatures = `[73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

Note: The length of temperatures will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

### Java Solution
```java
public int[] dailyTemperatures(int[] temperatures) {
    int[] result = new int[temperatures.length];
    for(int i = 0; i < temperatures.length; i++){
        int j = i + 1;
        while(j < temperatures.length && temperatures[j] <= temperatures[i])
            j++;
        if(j != temperatures.length)
            result[i] = j - i;
        else
            result[i] = 0;
    }
    return result;
}
```