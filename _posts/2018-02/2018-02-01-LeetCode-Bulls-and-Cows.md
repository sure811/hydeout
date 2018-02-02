---
layout: post
title: LeetCode - Bulls and Cows
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.
<!--more-->
For example:
```
Secret number:  "1807"
Friend's guess: "7810"
```
Hint: 1 bull and 3 cows. (The bull is 8, the cows are 0, 1 and 7.)
Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. In the above example, your function should return "1A3B".

Please note that both secret number and friend's guess may contain duplicate digits, for example:
```
Secret number:  "1123"
Friend's guess: "0111"
```
In this case, the 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow, and your function should return "1A1B".
You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.
### Java Solution
```java
public String getHint(String secret, String guess) {
    Map<Character, Integer> map = new HashMap<>();
    Set<Integer> set = new HashSet<>();
    int A = 0;
    for(int i = 0; i < secret.length(); i++){
        if(secret.charAt(i) == guess.charAt(i)){
            set.add(i);
            A++;
        } else{
            map.putIfAbsent(secret.charAt(i), 0);
            map.put(secret.charAt(i), map.get(secret.charAt(i)) + 1);
        }
    }

    int B = 0;
    for(int i = 0; i < guess.length(); i++){
        char c = guess.charAt(i);
        if(!set.contains(i) && map.containsKey(c)){
            B++;
            if(map.get(c) == 1)
                map.remove(c);
            else
                map.put(c, map.get(c) - 1);
        }
    }
    return A + "A" + B + "B";
}
```