---
layout: post
title: LeetCode - Implement Trie (Prefix Tree)
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Implement a trie with insert, search, and startsWith methods.
<!--more-->
**Note:**
You may assume that all inputs are consist of lowercase letters a-z.
### Java Solution
```java
class Trie {
    TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode(null);
    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++) {
            if(cur.children.containsKey(word.charAt(i)))
                cur = cur.children.get(word.charAt(i));
            else{
                TrieNode newNode = new TrieNode(word.substring(0, i + 1));
                cur.children.put(word.charAt(i), newNode);
                cur = newNode;
            }
        }
        cur.isLeaf = true;
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++) {
            if(cur.children.containsKey(word.charAt(i)))
                cur = cur.children.get(word.charAt(i));
            else{
                return false;
            }
        }
        return cur.isLeaf;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode cur = root;
        for(int i = 0; i < prefix.length(); i++) {
            if(cur.children.containsKey(prefix.charAt(i)))
                cur = cur.children.get(prefix.charAt(i));
            else{
                return false;
            }
        }
        return true;
    }

    class TrieNode {
        String root;
        boolean isLeaf;
        Map<Character, TrieNode> children;
        public TrieNode(String root) {
            this.root = root;
            children = new HashMap<>();
        }
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```