---
layout: post
title: LeetCode - Course Schedule
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Depth-first Search
excerpt_separator: "<!--more-->"
---

### Question Definition
There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?
<!--more-->
For example:
```
2, [[1,0]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.
```
2, [[1,0],[0,1]]
```
There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Note:**
1. The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
2. You may assume that there are no duplicate edges in the input prerequisites.
### Java Solution
```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    int[] preCourses = new int[numCourses];

    for(int[] pre : prerequisites){
        preCourses[pre[1]]++;
    }

    boolean[] visited = new boolean[numCourses];
    int ready = 0;
    while(ready <= numCourses) {
        boolean hasCourse = false;
        for(int i = 0; i < preCourses.length; i++){
            if(!visited[i] && preCourses[i] <= 0){
                visited[i] = true;
                ready++;
                hasCourse = true;
                for(int[] pre : prerequisites){
                    if(pre[0] == i)
                        preCourses[pre[1]]--;
                }
            }
        }
        if(!hasCourse) break;
    }
    return ready == numCourses;
}
```