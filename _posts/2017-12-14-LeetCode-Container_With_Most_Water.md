---
layout: post
title: LeetCode - Container With Most Water
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
<!--more-->

**Note:** You may not slant the container and n is at least 2.

### Java Solution
```java
    public int maxArea(int[] height) {
        int max = 0;
        int left = 0;
        int right = height.length - 1;
        while(left < right){
            if(height[left] < height[right]){
                int area = (right - left) * height[left];
                if(area > max)
                    max = area;
                left++;
            } else {
                int area = (right - left) * height[right];
                if(area > max)
                    max = area;
                right--;
            }
        }
        return max;
    }
```