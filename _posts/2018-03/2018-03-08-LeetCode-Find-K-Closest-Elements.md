---
layout: post
title: LeetCode - Find K Closest Elements
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
    int index =  -1;
    int min = Integer.MAX_VALUE;
    for(int i = 0; i < arr.length; i++){
        if(Math.abs(arr[i] - x) < min){
            min = Math.abs(arr[i] - x);
            index = i;
        }
    }
    List<Integer> result = new LinkedList<>();
    if(index == -1){
        if(arr[0] < x) index = arr.length;
    }else
        result.add(arr[index]);
    int left = index - 1;
    int right = index + 1;
    while(result.size() != k){
        if(left < 0) result.add(arr[right++]);
        else if(right >= arr.length) result.add(arr[left--]);
        else{
            if(Math.abs(arr[left] - x) <= Math.abs(arr[right] - x)){
                result.add(arr[left--]);
            }else if(Math.abs(arr[left] - x) > Math.abs(arr[right] - x)){
                result.add(arr[right++]);
            }
        }
    }
    Collections.sort(result);
    return result;
}
```