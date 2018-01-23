---
layout: post
title: LeetCode - Triangle
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.
<!--more-->

For example, given the following triangle
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
### Java Solution
```java
public int minimumTotal(List<List<Integer>> triangle) {
    if(triangle.size() == 0 || triangle.get(0).size() == 0) return 0;
    int[] maxs = new int[triangle.size()];
    maxs[0] = triangle.get(0).get(0);
    for(int level = 1; level < triangle.size(); level++){
        List<Integer> l = triangle.get(level);
        maxs[l.size() - 1] = maxs[l.size() - 2] + l.get(l.size() - 1);
        for(int i = l.size() - 2; i > 0; i--){
            maxs[i] = Math.min(maxs[i], maxs[i - 1]) + l.get(i);
        }
        maxs[0] = maxs[0] + l.get(0);
    }
    int min = maxs[0];
    for(int num : maxs){
        if(min > num)
            min = num;
    }
    return min;
}
```