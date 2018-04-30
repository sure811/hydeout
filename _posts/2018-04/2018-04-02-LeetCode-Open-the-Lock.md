---
layout: post
title: LeetCode - Open the Lock
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Breadth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
You have a lock in front of you with 4 circular wheels. Each wheel has 10 slots: '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'. The wheels can rotate freely and wrap around: for example we can turn '9' to be '0', or '0' to be '9'. Each move consists of turning one wheel one slot.

The lock initially starts at '0000', a string representing the state of the 4 wheels.

You are given a list of deadends dead ends, meaning if the lock displays any of these codes, the wheels of the lock will stop turning and you will be unable to open it.

Given a target representing the value of the wheels that will unlock the lock, return the minimum total number of turns required to open the lock, or -1 if it is impossible.
<!--more-->

**Example 1:**
```
Input: deadends = ["0201","0101","0102","1212","2002"], target = "0202"
Output: 6
Explanation:
A sequence of valid moves would be "0000" -> "1000" -> "1100" -> "1200" -> "1201" -> "1202" -> "0202".
Note that a sequence like "0000" -> "0001" -> "0002" -> "0102" -> "0202" would be invalid,
because the wheels of the lock become stuck after the display becomes the dead end "0102".
```
**Example 2:**
```
Input: deadends = ["8888"], target = "0009"
Output: 1
Explanation:
We can turn the last wheel in reverse to move from "0000" -> "0009".
```
**Example 3:**
```
Input: deadends = ["8887","8889","8878","8898","8788","8988","7888","9888"], target = "8888"
Output: -1
Explanation:
We can't reach the target without getting stuck.
```
**Example 4:**
```
Input: deadends = ["0000"], target = "8888"
Output: -1
```
**Note:**
1. The length of deadends will be in the range `[1, 500]`.
2. target will not be in the list deadends.
3. Every string in deadends and the string target will be a string of 4 digits from the 10,000 possibilities '0000' to '9999'.
### Java Solution
```java
class Solution {
    public int openLock(String[] deadends, String target) {
        Set<String> set = new HashSet<String>();
        for (String str:deadends) set.add(str);
        Queue<String> q = new LinkedList<String>();
        Set<String> visited = new HashSet<String>();
        Map<String, Integer> map = new HashMap<String, Integer>();
        q.add("0000");
        map.put("0000", 0);
        while (!q.isEmpty()) {
            String ss = q.poll();
            char[] arr1 = ss.toCharArray();
            char[] arr2 = ss.toCharArray();
            if (set.contains(ss)) continue;
            if (ss.equals(target)) return map.get(ss);
            for (int i = 0;i < arr1.length;i++) {
                int digit = arr1[i] - '0';
                if (digit + 1 > 9) arr1[i] = '0';
                else  arr1[i] = (char)((digit + 1) + '0');
                String next = String.valueOf(arr1);
                if (!visited.contains(next)) {
                    q.add(next);
                    visited.add(next);
                    map.put(next, map.get(ss) + 1);
                }
                arr1[i] = (char)(digit + '0');
            }
            for (int i = 0;i < arr2.length;i++) {
                int digit = arr2[i] - '0';
                if (digit - 1 < 0) arr2[i] = '9';
                else  arr2[i] = (char)((digit - 1) + '0');
                String next = String.valueOf(arr2);
                if (!visited.contains(next)) {
                    q.add(next);
                    visited.add(next);
                    map.put(next, map.get(ss) + 1);
                }
                arr2[i] = (char)(digit + '0');
            }
        }
        return -1;
    }
}
```