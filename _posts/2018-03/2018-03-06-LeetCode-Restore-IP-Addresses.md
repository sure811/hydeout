---
layout: post
title: LeetCode - Restore IP Addresses
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
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
    restoreIpAddressesHelper(s, 4, "", result);
    return result;
}

private void restoreIpAddressesHelper(String s, int length, String cur, List<String> result){
    if(length == 1){
        if(s.length() > 0 && s.length() < 4 && Integer.parseInt(s) < 256 && s.equals(Integer.toString(Integer.parseInt(s)))){
            cur += s;
            result.add(cur);
        }
        return;
    }
    if(s.length() > 1)
        restoreIpAddressesHelper(s.substring(1), length - 1, cur + s.substring(0, 1) + ".", result);
    if(s.length() > 2 && s.charAt(0) != '0')
        restoreIpAddressesHelper(s.substring(2), length - 1, cur + s.substring(0, 2) + ".", result);
    if(s.length() > 3 && Integer.parseInt(s.substring(0, 3)) > 99 && Integer.parseInt(s.substring(0, 3)) < 256)
        restoreIpAddressesHelper(s.substring(3), length - 1, cur + s.substring(0, 3) + ".", result);
}
```