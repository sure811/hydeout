---
layout: post
title: LeetCode - Kth Largest Element in an Array
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Heap
excerpt_separator: "<!--more-->"
---

### Question Definition
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example,
Given `[3,2,1,5,6,4]` and k = 2, return 5.

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.
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

    private void swap(int[] nums,int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
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
}
```