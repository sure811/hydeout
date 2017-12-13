---
layout: post
title: `[LeetCode]` Best Time to Buy and Sell Stock with Transaction Fee
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Array
    - Dynamic Programming
---

### Question Definition

Your are given an array of integers prices, for which the i-th element is the price of a given stock on day i; and a non-negative integer fee representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

**Example 1:**
```
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
* Buying at prices[0] = 1
* Selling at prices[3] = 8
* Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```
**Note**:

* 0 < prices.length <= 50000.
* 0 < prices`[i]` < 50000.
* 0 <= fee < 50000.

### Analysis
```
1. Hold stock:
* We do nothing on day i: hold[i - 1];
* We buy stock on day i: notHold[i - 1] - prices[i - 1] - fee;

2. Not hold stock:
* We do nothing on day i: notHold[i - 1];
* We sell stock on day i: hold[i - 1] + prices[i - 1];
```
### Java Solution
```java
    public int maxProfit(int[] prices, int fee) {
        int[] hold = new int[prices.length + 1];
        int[] noHold = new int[prices.length + 1];
        hold[0] = Integer.MIN_VALUE;

        for(int i = 1; i <= prices.length; i++){
            hold[i] = Math.max(hold[i - 1], noHold[i - 1] - prices[i - 1] - fee);
            noHold[i] = Math.max(noHold[i - 1], hold[i - 1] + prices[i - 1]);
        }
        return noHold[prices.length];
    }
```
