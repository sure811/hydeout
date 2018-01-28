---
layout: post
title: LeetCode - Validate IP Address
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
Write a function to check whether an input string is a valid IPv4 address or IPv6 address or neither.
<!--more-->

IPv4 addresses are canonically represented in dot-decimal notation, which consists of four decimal numbers, each ranging from 0 to 255, separated by dots ("."), e.g.,172.16.254.1;

Besides, leading zeros in the IPv4 is invalid. For example, the address 172.16.254.01 is invalid.

IPv6 addresses are represented as eight groups of four hexadecimal digits, each group representing 16 bits. The groups are separated by colons (":"). For example, the address 2001:0db8:85a3:0000:0000:8a2e:0370:7334 is a valid one. Also, we could omit some leading zeros among four hexadecimal digits and some low-case characters in the address to upper-case ones, so 2001:db8:85a3:0:0:8A2E:0370:7334 is also a valid IPv6 address(Omit leading zeros and using upper cases).

However, we don't replace a consecutive group of zero value with a single empty group using two consecutive colons (::) to pursue simplicity. For example, 2001:0db8:85a3::8A2E:0370:7334 is an invalid IPv6 address.

Besides, extra leading zeros in the IPv6 is also invalid. For example, the address 02001:0db8:85a3:0000:0000:8a2e:0370:7334 is invalid.

Note: You may assume there is no extra space or special characters in the input string.

Example 1:
```
Input: "172.16.254.1"

Output: "IPv4"

Explanation: This is a valid IPv4 address, return "IPv4".
```
Example 2:
```
Input: "2001:0db8:85a3:0:0:8A2E:0370:7334"

Output: "IPv6"

Explanation: This is a valid IPv6 address, return "IPv6".
```
Example 3:
```
Input: "256.256.256.256"

Output: "Neither"

Explanation: This is neither a IPv4 address nor a IPv6 address.
```
### Java Solution
```java
public class Solution {
    public String validIPAddress(String IP) {
        if(IP.equals("")) return "Neither";
        if(isIP4(IP)) return "IPv4";
        if(isIP6(IP)) return "IPv6";
        return "Neither";
    }

    public boolean isIP4(String IP){
        if(IP.charAt(0)=='.' || IP.charAt(IP.length()-1)=='.')return false;
        String[] temp = IP.split("\\.");
        if(temp.length!=4)return false;
        for(int i=0;i<4;i++){
            try{
                if(temp[i].startsWith("0")&&temp[i].length()>1) return false;
                if(Integer.parseInt(temp[i])>255 || temp[i].charAt(0)=='-' || temp[i].charAt(0)=='+')return false;
            }
            catch(NumberFormatException e){
                System.out.println("ERROR");
                return false;
            }
        }
        return true;
    }

    public boolean isIP6(String IP){
        if(IP.charAt(0)==':' || IP.charAt(IP.length()-1)==':')return false;
        String[] temp = IP.split(":");
        if(temp.length!=8)return false;
        for(int i=0;i<8;i++){
            if(temp[i].length()>4||temp[i].length()==0)return false;
            for(int j=0;j<temp[i].length();j++){
                if((temp[i].charAt(j)>='0' && temp[i].charAt(j)<='9') || (temp[i].charAt(j)>='a' && temp[i].charAt(j)<='f') || (temp[i].charAt(j)>='A' && temp[i].charAt(j)<='F')){}
                else return false;
            }
        }
        return true;
    }
}
```