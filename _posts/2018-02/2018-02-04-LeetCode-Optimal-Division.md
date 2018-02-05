---
layout: post
title: LeetCode - Optimal Division
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of positive integers, the adjacent integers will perform the float division. For example, [2,3,4] -> 2 / 3 / 4.

However, you can add any number of parenthesis at any position to change the priority of operations. You should find out how to add parenthesis to get the maximum result, and return the corresponding expression in string format. Your expression should NOT contain redundant parenthesis.
<!--more-->
**Example:**
```
Input: [1000,100,10,2]
Output: "1000/(100/10/2)"
Explanation:
1000/(100/10/2) = 1000/((100/10)/2) = 200
However, the bold parenthesis in "1000/((100/10)/2)" are redundant,
since they don't influence the operation priority. So you should return "1000/(100/10/2)".

Other cases:
1000/(100/10)/2 = 50
1000/(100/(10/2)) = 50
1000/100/10/2 = 0.5
1000/100/(10/2) = 2
```
**Note:**
1. The length of the input array is `[1, 10]`.
2. Elements in the given array will be in range `[2, 1000]`.
3. There is only one optimal division for each test case.
### Java Solution
```java
public String optimalDivision(int[] nums) {
    if (nums.length == 0) return "";
    String res = Integer.toString(nums[0]);
    if (nums.length == 1) return res;
    if (nums.length == 2) return res + "/" + Integer.toString(nums[1]);
    res += "/(" + Integer.toString(nums[1]);
    for (int i = 2; i < nums.length; ++i) {
        res += "/" + Integer.toString(nums[i]);
    }
    return res + ")";
}
```