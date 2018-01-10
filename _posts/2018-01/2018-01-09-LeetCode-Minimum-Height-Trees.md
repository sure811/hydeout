---
layout: post
title: LeetCode - Minimum Height Trees
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Breadth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
For a undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

**Format**
The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in edges.

**Example 1:**

Given n = 4, edges = `[[1, 0], [1, 2], [1, 3]]`
```
        0
        |
        1
       / \
      2   3
```
return `[1]`

**Example 2:**

Given n = 6, edges = `[[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]`
```
     0  1  2
      \ | /
        3
        |
        4
        |
        5
```
return `[3, 4]`

**Note:**

(1) According to the definition of tree on Wikipedia: “a tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.”

(2) The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.


### Java Solution
```java
class Solution {
    Map<Integer, Linked<Integer>> map = new HashMap<>();
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        for(int[] edge : edges){
            map.putIfAbsent(edge[0], new LinkedList<>());
            map.put(edge[0]).add(edge[1]);
            map.putIfAbsent(edge[1], new LinkedList<>());
            map.put(edge[1]).add(edge[0]);
        }
        int min = Integer.MAX_VALUE;
        List<Integer> result = new LinkedList<>();
        for(int i = 0; i < n; i++){
            int height = findHeight(n, edges, i);
            if(height < min){
                result.clear();
                result.add(i);
                min = height;
            }else if(height == min){
                result.add(i);
            }
        }
        return result;
    }

    private int findHeight(int n, int root){
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n];

    }
}
```