---
layout: post
title: DataStructure - Graph - Base
categories:
    - DataStructure
tags:
    - DataStructure
    - Graph
excerpt_separator: "<!--more-->"
---

### Graph

```java
import java.util.LinkedList;
import java.util.List;

public class Graph {
    private final int V; // number of vertices
    private int E; // number of edges
    private List<Integer>[] adj; // adjacency lists

    public Graph(int V) {
        this.V = V;
        this.E = 0;
        adj = new LinkedList[V]; // Create array of lists.
        for (int v = 0; v < V; v++) // Initialize all lists
            adj[v] = new LinkedList<Integer>(); // to empty.
    }

    public int V() {
        return V;
    }

    public int E() {
        return E;
    }

    public void addEdge(int v, int w) {
        adj[v].add(w); // Add w to v’s list.
        adj[w].add(v); // Add v to w’s list.
        E++;
    }

    public Iterable<Integer> adj(int v) {
        return adj[v];
    }
}
```