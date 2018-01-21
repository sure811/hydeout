---
layout: post
title: LeetCode - Sort Colors
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.
<!--more-->
**Note:**
You are not suppose to use the library's sort function for this problem.

**Follow up:**
A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?
### My Java Solution
```java
public void sortColors(int[] nums) {
    int end0 = -1;
    int start1 = -1;
    int start2 = -1;
    for(int i = 0; i < nums.length; i++){
        if(nums[i] == 0){
            if(start2 > -1)
                nums[i] = 2;
            else if(start1 > -1)
                nums[i] = 1;
            if(start1 > -1 && start2 > -1){
                nums[start2++] = 1;
            }
            if(start1 > -1)
                nums[start1++] = 0;
            else if(start2 > -1)
                nums[start2++] = 0;
        } else if(nums[i] == 1){
            if(start2 > -1){
                nums[i] = 2;
                nums[start2++] = 1;
                if(start1 == -1)
                    start1 = start2 - 1;
            }else if(start1 == -1)
                start1 = i;
        } else {
            if(start2 == -1)
                start2 = i;
        }
    }
}
```
### Best Java Solution
```java
public void sortColors(int[] nums) {
    // 1-pass
    int p1 = 0, p2 = nums.length - 1, index = 0;
    while (index <= p2) {
        if (nums[index] == 0) {
            nums[index] = nums[p1];
            nums[p1] = 0;
            p1++;
        }
        if (nums[index] == 2) {
            nums[index] = nums[p2];
            nums[p2] = 2;
            p2--;
            index--;
        }
        index++;
    }
}
```