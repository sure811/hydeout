---
layout: post
title: LeetCode - Maximum Length of Pair Chain
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
You are given n pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair (c, d) can follow another pair (a, b) if and only if b < c. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.
<!--more-->

**Example 1:**
```
Input: [[1,2], [2,3], [3,4]]
Output: 2
Explanation: The longest chain is [1,2] -> [3,4]
```
**Note:**
1. The number of given pairs will be in the range `[1, 1000]`.
### Java Solution
```java
public int findLongestChain(int[][] pairs) {
    int[] dp = new int[pairs.length];
    List<Integer[]> result = new LinkedList<>();
    for(int[] pair : pairs){
        result.add(new Integer[]{pair[0], pair[1]});
    }
    result.sort((a, b) -> a[1] == b[1] ? a[0] - b[0] : a[1] - b[1]);
    Deque<Integer[]> deque = new ArrayDeque<>();
    for(Integer[] pair : result){
        if (deque.isEmpty()) deque.push(pair);
        else {
            int t = deque.peek()[1];
            if (pair[0] > t) deque.push(pair);
        }
    }
    return deque.size();
}
```