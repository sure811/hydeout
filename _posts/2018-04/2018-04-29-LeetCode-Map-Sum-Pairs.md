---
layout: post
title: LeetCode - Map Sum Pairs
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Implement a MapSum class with insert, and sum methods.

For the method insert, you'll be given a pair of (string, integer). The string represents the key and the integer represents the value. If the key already existed, then the original key-value pair will be overridden to the new one.

For the method sum, you'll be given a string representing the prefix, and you need to return the sum of all the pairs' value whose key starts with the prefix.
<!--more-->
**Example 1:**
```
Input: insert("apple", 3), Output: Null
Input: sum("ap"), Output: 3
Input: insert("app", 2), Output: Null
Input: sum("ap"), Output: 5
```
### Java Solution
```java
class MapSum {
    TrieNode root;
    Set<String> set;

    /** Initialize your data structure here. */
    public MapSum() {
        root = new TrieNode(0);
        set = new HashSet<>();
    }

    public void insert(String key, int val) {
        TrieNode cur = root;
        for(int i = 0; i < key.length(); i++) {
            if(cur.children.containsKey(key.charAt(i))){
                cur = cur.children.get(key.charAt(i));
                if(set.contains(key))
                    cur.value = val;
                else
                    cur.value += val;
            }else{
                TrieNode newNode = new TrieNode(val);
                cur.children.put(key.charAt(i), newNode);
                cur = newNode;
            }
        }
        set.add(key);
    }

    public int sum(String prefix) {
        TrieNode cur = root;
        for(int i = 0; i < prefix.length(); i++) {
            if(cur.children.containsKey(prefix.charAt(i)))
                cur = cur.children.get(prefix.charAt(i));
            else{
                return 0;
            }
        }
        return cur.value;
    }

    class TrieNode {
        int value;
        Map<Character, TrieNode> children;
        public TrieNode(int value) {
            this.value = value;
            children = new HashMap<>();
        }
    }
}

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum obj = new MapSum();
 * obj.insert(key,val);
 * int param_2 = obj.sum(prefix);
 */
```