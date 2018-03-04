---
layout: post
title: LeetCode - Rectangle Area
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Find the total area covered by two rectilinear rectangles in a 2D plane.
<!--more-->

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

Assume that the total area is never beyond the maximum possible value of int.
### Java Solution
```java
public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
    int width = 0;
    int height = 0;
    if(A <= E && C > E) width = Math.min(C, G) - E;
    else if(A > E && A < G) width = Math.min(C, G) - A;

    if(B <= F && D > F) height = Math.min(D, H) - F;
    else if(B > F && B < H) height = Math.min(D, H) - B;
    System.out.println(height);
    System.out.println(width);
    return (C-A) * (D-B) + (G-E) * (H-F) - width * height;
}
```