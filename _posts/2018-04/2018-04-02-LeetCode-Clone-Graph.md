---
layout: post
title: LeetCode - Clone Graph
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.
<!--more-->

OJ's undirected graph serialization:
Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

1. First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
2. Second node is labeled as 1. Connect node 1 to node 2.
3. Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
Visually, the graph looks like the following:
```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```
### Java Solution
```java
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node == null) return null;
        Map<UndirectedGraphNode, UndirectedGraphNode> graph = new HashMap<>();

        return dfs(node, graph);
    }

    private UndirectedGraphNode dfs(UndirectedGraphNode node, Map<UndirectedGraphNode, UndirectedGraphNode> graph){
        if(graph.containsKey(node)) return graph.get(node);
        UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);

        graph.put(node, newNode);
        for(UndirectedGraphNode nei : node.neighbors) {
            newNode.neighbors.add(dfs(nei, graph));
        }
        return newNode;
    }
}
```