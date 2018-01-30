---
layout: post
title: LeetCode - Can I Win
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
In the "100 game," two players take turns adding, to a running total, any integer from 1..10. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?

For example, two players might take turns drawing from a common pool of numbers of 1..15 without replacement until they reach a total >= 100.

Given an integer maxChoosableInteger and another integer desiredTotal, determine if the first player to move can force a win, assuming both players play optimally.

You can always assume that maxChoosableInteger will not be larger than 20 and desiredTotal will not be larger than 300.
<!--more-->
**Example**
```
Input:
maxChoosableInteger = 10
desiredTotal = 11

Output:
false

Explanation:
No matter which integer the first player choose, the first player will lose.
The first player can choose an integer from 1 up to 10.
If the first player choose 1, the second player can only choose integers from 2 up to 10.
The second player will win by choosing 10 and get a total = 11, which is >= desiredTotal.
Same with other integers chosen by the first player, the second player will always win.
```
### Java Solution
```java
public boolean canIWin(int maxChoosableInteger, int desiredTotal) {
    if (maxChoosableInteger >= desiredTotal) return true;
    if (maxChoosableInteger * (maxChoosableInteger + 1) / 2 < desiredTotal) return false;
    Map<Integer, Boolean> m = new HashMap<>();
    return canWin(maxChoosableInteger, desiredTotal, 0, m);
}

private boolean canWin(int length, int total, int used, Map<Integer, Boolean> m) {
    if (m.containsKey(used)) return m.get(used);
    for (int i = 0; i < length; ++i) {
        int cur = (1 << i);
        if ((cur & used) == 0) {
            if (total <= i + 1 || !canWin(length, total - (i + 1), cur | used, m)) {
                m.put(used, true);
                return true;
            }
        }
    }
    m.put(used, false);
    return false;
}
```