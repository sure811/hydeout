---
layout: post
title: LeetCode - Shuffle an Array
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Shuffle a set of numbers without duplicates.
<!--more-->
**Example:**
```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```
### Java Solution
```java
class Solution {
    private int[] nums;
    private Random random;

    public Solution(int[] nums) {
        this.nums = nums;
        random = new Random();
    }

    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }

    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        List<Integer> list = new LinkedList<>();
        for(int num : nums)
            list.add(num);
        int[] shuffers = new int[nums.length];
        int i = 0;
        while(i < nums.length) {
            int randomIndex = random.nextInt(list.size());
            shuffers[i] = list.get(randomIndex);
            list.remove(randomIndex);
            i++;
        }
        return shuffers;
    }
}
```