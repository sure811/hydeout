---
layout: post
title: LeetCode - Implement Magic Dictionary
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
Implement a magic directory with buildDict, and search methods.

For the method buildDict, you'll be given a list of non-repetitive words to build a dictionary.

For the method search, you'll be given a word, and judge whether if you modify exactly one character into another character in this word, the modified word is in the dictionary you just built.

**Example 1:**
```
Input: buildDict(["hello", "leetcode"]), Output: Null
Input: search("hello"), Output: False
Input: search("hhllo"), Output: True
Input: search("hell"), Output: False
Input: search("leetcoded"), Output: False
```
**Note:**
1. You may assume that all the inputs are consist of lowercase letters a-z.
2. For contest purpose, the test data is rather small by now. You could think about highly efficient algorithm after the contest.
3. Please remember to RESET your class variables declared in class MagicDictionary, as static/class variables are persisted across multiple test cases. Please see here for more details.
### Java Solution
```java
class MagicDictionary {
    Map<Integer, List<String>> map;
    /** Initialize your data structure here. */
    public MagicDictionary() {
        map = new HashMap<>();
    }

    /** Build a dictionary through a list of words */
    public void buildDict(String[] dict) {
        for(String d : dict){
            map.putIfAbsent(d.length(), new LinkedList<>());
            map.get(d.length()).add(d);
        }
    }

    /** Returns if there is any word in the trie that equals to the given word after modifying exactly one character */
    public boolean search(String word) {
        if(!map.containsKey(word.length()))
            return false;
        for(String s : map.get(word.length())){
            boolean diff = false;
            int i = 0;
            for(; i < s.length(); i++){
                if(s.charAt(i) != word.charAt(i)){
                    if(diff){
                        break;
                    }else{
                        diff = true;
                    }
                }
            }
            if(diff && i == s.length())
                return true;
        }
        return false;
    }
}
```