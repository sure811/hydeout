---
layout: post
title: LeetCode - Evaluate Division
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
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
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        Map<String, Map<String, Double>> map = new HashMap<>();

        for(int i = 0; i < equations.length; i++) {
            String[] equation = equations[i];
            map.putIfAbsent(equation[0], new HashMap<>());
            map.putIfAbsent(equation[1], new HashMap<>());
            map.get(equation[0]).put(equation[1], values[i]);
            map.get(equation[1]).put(equation[0], 1 / values[i]);
        }

        double[] res = new double[queries.length];
        for(int i = 0; i < queries.length; i++) {
            if(!map.containsKey(queries[i][0]) || !map.containsKey(queries[i][1])){
                res[i] = -1.0;
                continue;
            }
            Set<String> visited = new HashSet<>();
            res[i] = dfs(map, queries[i][0], queries[i][1], visited, 1);
            if(res[i] == -1){
                visited = new HashSet<>();
                res[i] = 1 / dfs(map, queries[i][1], queries[i][0], visited, 1);
            }
        }
        return res;
    }

    private double dfs(Map<String, Map<String, Double>> map, String start, String end, Set<String> visited, double res){
        // System.out.println(start + ":" + end + "|" + res);
        if(start.equals(end)) return res;
        double result = -1.0;
        for(Map.Entry<String, Double> entry : map.get(start).entrySet()){
            if(!visited.contains(entry.getKey())){
                visited.add(entry.getKey());
                double _res = dfs(map, entry.getKey(), end, visited, res * entry.getValue());
                if(_res > -1 && (result == -1 || _res < result))
                    result = _res;
            }
        }
        return result;
    }
}
```