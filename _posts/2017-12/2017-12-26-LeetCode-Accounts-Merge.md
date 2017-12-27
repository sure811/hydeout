---
layout: post
title: LeetCode - Accounts Merge
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
Given a list accounts, each element `accounts[i]` is a list of strings, where the first element `accounts[i][0]` is a name, and the rest of the elements are emails representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails in sorted order. The accounts themselves can be returned in any order.
<!--more-->

**Example 1:**
```
Input:
accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]
Output: [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]
Explanation:
The first and third John's are the same person as they have the common email "johnsmith@mail.com".
The second John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'],
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```
**Note:**
1. The length of accounts will be in the range `[1, 1000]`.
2. The length of `accounts[i]` will be in the range `[1, 10]`.
3. The length of `accounts[i][j]` will be in the range `[1, 30]`.
### Java Solution
```java
public List<List<String>> accountsMerge(List<List<String>> accounts) {
    List<List<String>> res = new ArrayList<>();
    Map<String, Node> map = new HashMap<>();    // <Email, email node>

    // Build the graph;
    for (List<String> list : accounts) {
        for (int j = 1; j < list.size(); j++) {
            String email = list.get(j);

            if (!map.containsKey(email)) {
                Node node = new Node(email, list.get(0));
                map.put(email, node);
            }

            if (j == 1) continue;
            //Connect the current email node to the previous email node;
            map.get(list.get(j - 1)).neighbors.add(map.get(email));
            map.get(email).neighbors.add(map.get(list.get(j - 1)));
        }
    }

    // DFS search for each components(each account);
    Set<String> visited = new HashSet<>();
    for (String s : map.keySet()) {
        if (visited.add(s)) {
            List<String> list = new LinkedList<>();
            list.add(s);
            dfs(map.get(s), visited, list);
            Collections.sort(list);
            list.add(0, map.get(s).username);
            res.add(list);
        }
    }
    return res;
}

public void dfs(Node root, Set<String> visited, List<String> list) {
    for (Node node : root.neighbors) {
        if (visited.add(node.val)) {
            list.add(node.val);
            dfs(node, visited, list);
        }
    }
}

class Node {
    String val;         // Email address;
    String username;    // Username;
    List<Node> neighbors;
    Node(String val, String username) {
        this.val = val;
        this.username = username;
        neighbors = new ArrayList<>();
    }
}
```