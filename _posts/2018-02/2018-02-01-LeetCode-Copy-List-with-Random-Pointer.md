---
layout: post
title: LeetCode - Copy List with Random Pointer
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Hash Table
excerpt_separator: "<!--more-->"
---

### Question Definition
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.
<!--more-->
### Java Solution
```java
public RandomListNode copyRandomList(RandomListNode head) {
    if(head == null) return null;
    Map<RandomListNode, RandomListNode> map = new HashMap<>();
    RandomListNode newHead = null;
    RandomListNode pre = null;
    RandomListNode node = head;
    do{
        RandomListNode newNode = new RandomListNode(node.label);
        map.put(node, newNode);
        if(newHead == null) newHead = newNode;
        if(pre != null) pre.next = newNode;
        pre = newNode;
        node = node.next;
    }while(node != null);
    RandomListNode newNode = newHead;
    while(head != null){
        if(head.random != null){
            newNode.random = map.get(head.random);
        }
        head = head.next;
        newNode = newNode.next;
    }
    return newHead;
}
```