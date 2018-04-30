---
layout: post
title: LeetCode - Word Ladder
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Breadth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.
<!--more-->
**Example 1:**
```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```
**Example 2:**
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```
### Java Solution
```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Queue<String> q = new LinkedList<String>();
    Set<String> visited = new HashSet<String>();
    Map<String, Integer> map = new HashMap<String, Integer>();
    q.add(beginWord);
    map.put(beginWord, 1);
    while (!q.isEmpty()) {
        String ss = q.poll();
        if (ss.equals(endWord)) return map.get(ss);
        for(String word : wordList){
            if(!visited.contains(word) && word.length() == ss.length()){
                int different = 0;
                for(int i = 0; i < word.length(); i++){
                    if(word.charAt(i) != ss.charAt(i))
                        different++;
                }
                if(different == 1){
                    visited.add(word);
                    q.add(word);
                    map.put(word, map.get(ss) + 1);
                }
            }
        }
    }
    return 0;
}
```