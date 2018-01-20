---
layout: post
title: LeetCode - Find All Duplicates in an Array
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Array
excerpt_separator: "<!--more-->"
---

### Question Definition
Given an array of integers, `1 ≤ a[i] ≤ n` (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?
<!--more-->

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```
### My Java Solution
```java
public List<Integer> findDuplicates(int[] nums) {
    List<Integer> result = new LinkedList<>();

    for(int i = 0; i < nums.length; i++){
        if(nums[i] > 0 && nums[i] - 1 != i){
            int nextIndex = nums[i] - 1;
            nums[i] = 0;
            while(nextIndex >= 0 && nextIndex != nums[nextIndex] - 1){
                int temp = nextIndex;
                nextIndex = nums[nextIndex] - 1;
                nums[temp] = temp + 1;
            }
            if(nextIndex >= 0)
                result.add(nextIndex + 1);
        }
    }
    return result;
}
```

### Best Java Solution
```java
public List<Integer> findDuplicates(int[] nums) {
    List<Integer> res = new ArrayList<>();
    for (int i = 0; i < nums.length; ++i) {
        int index = Math.abs(nums[i])-1;
        if (nums[index] < 0)
            res.add(Math.abs(index+1));
        nums[index] = -nums[index];
    }
    return res;
}
```