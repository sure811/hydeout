---
layout: post
title: LeetCode - Find K Closest Elements
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Binary Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.
<!--more-->

**Example 1:**
```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```
**Example 2:**
```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```
**Note:**
1. The value k is positive and will always be smaller than the length of the sorted array.
2. Length of the given array is positive and will not exceed 104
3. Absolute value of elements in the array and x will not exceed 104
### Java Solution
```java
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    List<Integer> result = new LinkedList<>();
    if (arr.length == 0) return result;
    int left = 0;
    int right = arr.length - 1;
    while(left <= right){
        int mid = (left + right) / 2;
        if(arr[mid] == x){
            left = mid;
            break;
        }
        if(arr[mid] < x)
            left = mid + 1;
        else
            right = mid - 1;
    }
    left--;
    right = left + 1;
    while(k > 0 && (left >= 0 || right < arr.length)){
        if(left >= 0 && (right >= arr.length || x - arr[left] <= arr[right] - x)){
            result.add(0, arr[left]);
            k--;
            left--;
        }else{
            result.add(arr[right]);
            k--;
            right++;
        }
    }
    return result;
}
```