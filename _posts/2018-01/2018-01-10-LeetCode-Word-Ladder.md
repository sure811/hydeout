---
layout: post
title: LeetCode - Word Ladder
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Breadth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.

2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
<!--more-->
For example,

Given:
beginWord = "hit"
endWord = "cog"
wordList = `["hot","dot","dog","lot","log","cog"]`
As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.

Note:
* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.
### Java Solution
```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    if(wordList.size() == 0) return 0;

    Map<String, Boolean> visited = new HashMap<>();
    Queue<String> queue = new LinkedList<>();
    queue.add(beginWord);
    queue.add("");
    int level = 1;
    while(!queue.isEmpty()){
        String cur = queue.poll();
        if(cur.isEmpty()){
            level++;
            if(queue.isEmpty())
                return 0;
            else
                queue.add("");
        }else{
            if(cur.equals(endWord))
                return level;
            for(int j = 0; j < wordList.size(); j++){
                if(visited.containsKey(wordList.get(j)) || cur.length() != wordList.get(j).length())
                    continue;
                int one = 0;
                for(int k = 0; k < cur.length(); k++){
                    if(cur.charAt(k) != wordList.get(j).charAt(k)){
                        one++;
                        if(one == 2)
                            break;
                    }
                }
                if(one == 1){
                    queue.add(wordList.get(j));
                    visited.put(wordList.get(j), true);
                }
            }
        }
    }
    return 0;
}
```