---
layout: post
title: LeetCode - Minimum Genetic Mutation
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
excerpt_separator: "<!--more-->"
---

### Question Definition
A gene string can be represented by an 8-character long string, with choices from "A", "C", "G", "T".

Suppose we need to investigate about a mutation (mutation from "start" to "end"), where ONE mutation is defined as ONE single character changed in the gene string.

For example, "AACCGGTT" -> "AACCGGTA" is 1 mutation.

Also, there is a given gene "bank", which records all the valid gene mutations. A gene must be in the bank to make it a valid gene string.

Now, given 3 things - start, end, bank, your task is to determine what is the minimum number of mutations needed to mutate from "start" to "end". If there is no such a mutation, return -1.
<!--more-->

**Note:**
1. Starting point is assumed to be valid, so it might not be included in the bank.
2. If multiple mutations are needed, all mutations during in the sequence must be valid.
3. You may assume start and end string is not the same.
**Example 1:**
```
start: "AACCGGTT"
end:   "AACCGGTA"
bank: ["AACCGGTA"]

return: 1
```
**Example 2:**
```
start: "AACCGGTT"
end:   "AAACGGTA"
bank: ["AACCGGTA", "AACCGCTA", "AAACGGTA"]

return: 2
```
**Example 3:**
```
start: "AAAAACCC"
end:   "AACCCCCC"
bank: ["AAAACCCC", "AAACCCCC", "AACCCCCC"]

return: 3
```
### Java Solution
```java
public int minMutation(String start, String end, String[] bank) {
    Map<String, List<String>> graph = new HashMap<>();
    for(int i = 0; i < bank.length; i++){
        int diff = 0;
        for(int k = 0; k < bank[i].length(); k++){
            if(bank[i].charAt(k) != start.charAt(k))
                diff++;
            if(diff >= 2) break;
        }
        if(diff == 1){
            graph.putIfAbsent(start, new LinkedList<>());
            graph.get(start).add(bank[i]);
        }
        for(int j = i + 1; j < bank.length; j++){
            diff = 0;
            for(int k = 0; k < bank[i].length(); k++){
                if(bank[i].charAt(k) != bank[j].charAt(k))
                    diff++;
                if(diff >= 2) break;
            }
            if(diff == 1){
                graph.putIfAbsent(bank[i], new LinkedList<>());
                graph.putIfAbsent(bank[j], new LinkedList<>());
                graph.get(bank[i]).add(bank[j]);
                graph.get(bank[j]).add(bank[i]);
            }
        }
    }
    Set<String> visited = new HashSet<>();
    Deque<String> queue = new ArrayDeque<>();
    queue.add(start);
    queue.add("");
    int change = 0;
    while(!queue.isEmpty()){
        String node = queue.poll();
        visited.add(node);
        if(node.isEmpty()){
            if(queue.isEmpty()) return -1;
            change++;
            queue.add("");
        }else{
            if(node.equals(end)) return change;
            if(graph.containsKey(node))
                for(String edge : graph.get(node))
                    if(!visited.contains(edge))
                        queue.add(edge);
        }
    }
    return -1;
}
```