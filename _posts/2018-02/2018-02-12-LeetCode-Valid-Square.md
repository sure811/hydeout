---
layout: post
title: LeetCode - Valid Square
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given the coordinates of four points in 2D space, return whether the four points could construct a square.

The coordinate (x,y) of a point is represented by an integer array with two integers.
<!--more-->

Example:
```
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
Output: True
```

Note:
1. All the input integers are in the range `[-10000, 10000]`.
2. A valid square has four equal sides with positive length and four equal angles (90-degree angles).
3. Input points have no order.
### Java Solution
```java
public boolean validSquare(int[] p1, int[] p2, int[] p3, int[] p4) {
    double[] dis = new double[6];
    dis[0] = (p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]);
    dis[1] = (p1[0] - p4[0]) * (p1[0] - p4[0]) + (p1[1] - p4[1]) * (p1[1] - p4[1]);
    dis[2] = (p1[0] - p3[0]) * (p1[0] - p3[0]) + (p1[1] - p3[1]) * (p1[1] - p3[1]);
    dis[3] = (p2[0] - p3[0]) * (p2[0] - p3[0]) + (p2[1] - p3[1]) * (p2[1] - p3[1]);
    dis[4] = (p2[0] - p4[0]) * (p2[0] - p4[0]) + (p2[1] - p4[1]) * (p2[1] - p4[1]);
    dis[5] = (p3[0] - p4[0]) * (p3[0] - p4[0]) + (p3[1] - p4[1]) * (p3[1] - p4[1]);

    double max = Double.MAX_VALUE;
    double min = Double.MAX_VALUE;
    int count = 0;
    for(double num : dis){
        if(num == max)
            count++;
        else if(num == min)
            ;
        else if(max == Double.MAX_VALUE)
            max = num;
        else if(min == Double.MAX_VALUE)
            min = num;
        else
            return false;
    }
    return count == 3 || count == 1;
}
```