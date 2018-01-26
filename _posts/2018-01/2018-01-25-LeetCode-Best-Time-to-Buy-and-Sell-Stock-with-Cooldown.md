---
layout: post
title: LeetCode - Best Time to Buy and Sell Stock with Cooldown
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Dynamic Programming
excerpt_separator: "<!--more-->"
---

### Question Definition
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
<!--more-->
Example:
```
prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```
### Java Solution
```java
public int maxProfit(int[] prices) {
    if(prices.length == 0) return 0;
    int[] buy = new int[prices.length];
    int[] sell = new int[prices.length];
    buy[0] = - prices[0];
    for(int i = 1; i < prices.length; i++){
        buy[i] = Math.max((i > 1 ? sell[i - 2] : 0) - prices[i], buy[i - 1]);
        sell[i] = Math.max(buy[i - 1] + prices[i], (i > 1 ? sell[i - 1] : 0));
    }
    return Math.max(buy[prices.length - 1], sell[prices.length - 1]);
}
```