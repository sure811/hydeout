---
layout: post
title: LeetCode - Reconstruct Itinerary
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
    - Depth First Search
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list of airline tickets represented by pairs of departure and arrival airports `[from, to]`, reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.
<!--more-->

**Note:**
1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary `["JFK", "LGA"]` has a smaller lexical order than `["JFK", "LGB"]`.
2. All airports are represented by three capital letters (IATA code).
3. You may assume all tickets form at least one valid itinerary.

**Example 1:**

`tickets = [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]

Return ["JFK", "MUC", "LHR", "SFO", "SJC"].`

**Example 2:**

`tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]

Return ["JFK","ATL","JFK","SFO","ATL","SFO"].

Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.`
### Java Solution
```java
Map<String, PriorityQueue<String>> flights;
LinkedList<String> path;

public List<String> findItinerary(String[][] tickets) {
    flights = new HashMap<>();
    path = new LinkedList<>();
    for (String[] ticket : tickets) {
        flights.putIfAbsent(ticket[0], new PriorityQueue<>());
        flights.get(ticket[0]).add(ticket[1]);
    }
    dfs("JFK");
    return path;
}

public void dfs(String departure) {
    PriorityQueue<String> arrivals = flights.get(departure);
    while (arrivals != null && !arrivals.isEmpty())
        dfs(arrivals.poll());
    path.addFirst(departure);
}
```