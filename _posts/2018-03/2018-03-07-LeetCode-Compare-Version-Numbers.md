---
layout: post
title: LeetCode - Compare Version Numbers
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - String
excerpt_separator: "<!--more-->"
---

### Question Definition
Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.
<!--more-->

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:
```
0.1 < 1.1 < 1.2 < 13.37
```
### Java Solution
```java
public int compareVersion(String version1, String version2) {
    String[] v1 = version1.split("\\.");
    String[] v2 = version2.split("\\.");
    int i = 0;
    while(i < v1.length && i < v2.length){
        if(Integer.parseInt(v1[i]) > Integer.parseInt(v2[i]))
            return 1;
        if(Integer.parseInt(v1[i]) < Integer.parseInt(v2[i]))
            return -1;
        i++;
    }
    int length1 = v1.length;
    int length2 = v2.length;
    while(length1 > 0 && Integer.parseInt(v1[length1 - 1]) == 0) length1--;
    while(length2 > 0 && Integer.parseInt(v2[length2 - 1]) == 0) length2--;

    if(length1 > length2) return 1;
    if(length1 < length2) return -1;
    return 0;
}
```