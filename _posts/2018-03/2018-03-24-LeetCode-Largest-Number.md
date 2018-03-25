---
layout: post
title: LeetCode - Largest Number
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Sort
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of non negative integers, arrange them such that they form the largest number.
<!--more-->

For example, given `[3, 30, 34, 5, 9]`, the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.
### Java Solution
```java
public String largestNumber(int[] nums) {
    PriorityQueue<String> que = new PriorityQueue<String>((a, b)->
        (int)(Double.parseDouble(b + a) - Double.parseDouble(a + b))
    );

    for(int num : nums)
        que.offer(Integer.toString(num));
    String result = "";
    while(!que.isEmpty()){
        String num = que.poll();
        if(num.equals("0") && result.startsWith("0"))
            continue;
        result += num;
    }
    return result;
}
```