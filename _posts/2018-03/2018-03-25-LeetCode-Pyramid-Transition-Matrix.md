---
layout: post
title: LeetCode - Pyramid Transition Matrix
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Bit Manipulation
excerpt_separator: "<!--more-->"
---

### Question Definition
We are stacking blocks to form a pyramid. Each block has a color which is a one letter string, like `'Z'`.

For every block of color `C` we place not in the bottom row, we are placing it on top of a left block of color `A` and right block of color `B`. We are allowed to place the block there only if `(A, B, C)` is an allowed triple.

We start with a bottom row of bottom, represented as a single string. We also start with a list of allowed triples allowed. Each allowed triple is represented as a string of length 3.

Return true if we can build the pyramid all the way to the top, otherwise false.
<!--more-->

**Example 1:**
```
Input: bottom = "XYZ", allowed = ["XYD", "YZE", "DEA", "FFF"]
Output: true
Explanation:
We can stack the pyramid like this:
    A
   / \
  D   E
 / \ / \
X   Y   Z

This works because ('X', 'Y', 'D'), ('Y', 'Z', 'E'), and ('D', 'E', 'A') are allowed triples.
```
**Example 2:**
```
Input: bottom = "XXYX", allowed = ["XXX", "XXY", "XYX", "XYY", "YXZ"]
Output: false
Explanation:
We can't stack the pyramid to the top.
Note that there could be allowed triples (A, B, C) and (A, B, D) with C != D.
```
**Note:**
1. bottom will be a string with length in range `[2, 8]`.
2. allowed will have length in range `[0, 200]`.
3. Letters in all strings will be chosen from the set {'A', 'B', 'C', 'D', 'E', 'F', 'G'}.
### Java Solution
```java
public boolean pyramidTransition(String bottom, List<String> allowed) {
    Map<String, Set<Character>> map = new HashMap<>();
    for (String str : allowed) {
        map.putIfAbsent(str.charAt(0) + "" + str.charAt(1), new HashSet<>());
        map.get(str.charAt(0) + "" + str.charAt(1)).add(str.charAt(2));
    }
    return helper(bottom, "", map);
}
private boolean helper(String cur, String above, Map<String, Set<Character>> map) {
    if (cur.length() == 2 && above.length() == 1) return true;
    if (above.length() == cur.length() - 1) return helper(above, "", map);
    int pos = above.length();
    String base = cur.substring(pos, pos + 2);
    if (map.containsKey(base)) {
        for (char ch : map.get(base)) {
            if (helper(cur, above + ch, map)) {
                return true;
            }
        }
    }
    return false;
}
```