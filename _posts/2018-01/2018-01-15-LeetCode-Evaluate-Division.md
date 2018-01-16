---
layout: post
title: LeetCode - Evaluate Division
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Graph
excerpt_separator: "<!--more-->"
---

### Question Definition
Equations are given in the format A / B = k, where A and B are variables represented as strings, and k is a real number (floating point number). Given some queries, return the answers. If the answer does not exist, return -1.0.
<!--more-->

Example:
Given a / b = 2.0, b / c = 3.0.
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? .
return `[6.0, 0.5, -1.0, 1.0, -1.0 ]`.

The input is: vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries , where equations.size() == values.size(), and the values are positive. This represents the equations. Return vector<double>.

According to the example above:
```
equations = [ ["a", "b"], ["b", "c"] ],
values = [2.0, 3.0],
queries = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ].
```
The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.
### Java Solution
```java
class Solution {
    private Map<String, List<Object[]>> graph;
    private Set<String> visited;
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        graph = new HashMap<>();
        visited = new HashSet<>();
        for(int i = 0; i < equations.length; i++) {
            String[] equation = equations[i];
            graph.putIfAbsent(equation[0], new LinkedList<>());
            graph.putIfAbsent(equation[1], new LinkedList<>());
            graph.get(equation[0]).add(new Object[]{equation[1], values[i]});
            graph.get(equation[1]).add(new Object[]{equation[0], 1.0 / values[i]});
        }
        double[] result = new double[queries.length];
        for(int i = 0; i < queries.length; i++){
            result[i] = gfs(queries[i][0], queries[i][1]);
            visited.clear();
        }
        return result;
    }

    private double gfs(String start, String end){
        if(!graph.containsKey(start) || !graph.containsKey(end))
            return -1;
        if(start.equals(end)) return 1.0;
        for(int i = 0; i < graph.get(start).size(); i++){
            String edge = (String)graph.get(start).get(i)[0];
            if(edge.equals(end)) return (double)graph.get(start).get(i)[1];
            if(!visited.contains(edge)){
                visited.add(edge);
                double temp = gfs(edge, end);
                if(temp != -1)
                    return (double)graph.get(start).get(i)[1] * temp;
            }
        }
        return -1;
    }
}
```