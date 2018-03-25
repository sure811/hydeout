---
layout: post
title: LeetCode - Wiggle Sort II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Sort
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an unsorted array nums, reorder it such that `nums[0] < nums[1] > nums[2] < nums[3]....`
<!--more-->

**Example:**
(1) Given nums = `[1, 5, 1, 1, 6, 4]`, one possible answer is `[1, 4, 1, 5, 1, 6]`.
(2) Given nums = `[1, 3, 2, 2, 3, 1]`, one possible answer is `[2, 3, 1, 3, 1, 2]`.

**Note:**
You may assume all input has valid answer.

**Follow Up:**
Can you do it in O(n) time and/or in-place with O(1) extra space?


### Java Solution
```java
class Solution {
    public void wiggleSort(int[] nums) {
        int median = findKthLargest(nums, (nums.length + 1) / 2);
        int n = nums.length;

        int left = 0, i = 0, right = n - 1;

        while (i <= right) {

            if (nums[newIndex(i,n)] > median) {
                swap(nums, newIndex(left++,n), newIndex(i++,n));
            }
            else if (nums[newIndex(i,n)] < median) {
                swap(nums, newIndex(right--,n), newIndex(i,n));
            }
            else {
                i++;
            }
        }


    }

    private int newIndex(int index, int n) {
        return (1 + 2*index) % (n | 1);
    }

    private int findKthLargest(int[] nums, int k) {
        int start = 0;
        int end = nums.length - 1;
        while(true){
            int partition = partition(nums, start, end);
            if(partition == k - 1)
                return nums[partition];
            else if(partition > k - 1){
                end = partition - 1;
            }else{
                start = partition + 1;
            }
        }
    }

    private int partition(int[] a, int lo, int hi){
        int i = lo, j = hi+1; // left and right scan indices
        int v = a[lo]; // partitioning item
        while (true)
        { // Scan right, scan left, check for scan complete, and exchange.
            while (++i < hi && a[i] > v);
            while (--j > lo && v > a[j]) if (j == lo) break;
            if (i >= j) break;
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
        int temp = a[lo];
        a[lo] = a[j];
        a[j] = temp;
        return j;
    }

    private void swap(int[] nums,int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```