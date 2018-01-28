---
layout: post
title: LeetCode - Transpose File
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Shell
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a text file file.txt, transpose its content.

You may assume that each row has the same number of columns and each field is separated by the ' ' character.

For example, if file.txt has the following content:
```
name age
alice 21
ryan 30
```
Output the following:
```
name alice ryan
age 21 30
```
### Java Solution
```java
awk '
    {
        for(i=1; i<=NF; i++)
        {
            if(line[i] == "")
            {
                line[i] = $i
            }
            else
            {
                line[i] = line[i]" "$i
            }
        }
    }
    END{
         for(i=1; i<=NF; i++)
         {
             print line[i]
         }
       }
    ' file.txt
```