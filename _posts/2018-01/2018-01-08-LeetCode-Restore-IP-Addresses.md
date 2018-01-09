---
layout: post
title: LeetCode - Restore IP Addresses
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Backtracking
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a string containing only digits, restore it by returning all possible valid IP address combinations.
<!--more-->

For example:
Given "25525511135",

return `["255.255.11.135", "255.255.111.35"]`. (Order does not matter)
### Java Solution
```java
public List<String> restoreIpAddresses(String s) {
    List<String> result = new LinkedList<>();
    if(s.length() == 0 || s.length() > 12) return result;
    restoreIpAddressesHelper(s, 0, 4, "", result);
    return result;
}

private void restoreIpAddressesHelper(String s, int start, int num, String cur, List<String> result){
    if(num == 0 && start == s.length()){
        cur = cur.substring(0, cur.length() - 1);
        result.add(cur);
        return;
    }

    for(int i = start + 1; i <= s.length(); i++){
        String sub = s.substring(start, i);
        int digit = Integer.parseInt(sub);
        if(digit > 255) break;
        restoreIpAddressesHelper(s, i, num - 1, cur + sub + ".", result);
        if(digit == 0) break;
    }
}
```