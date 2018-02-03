---
layout: post
title: LeetCode - Partition List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.
<!--more-->

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.
### Java Solution
```java
public ListNode partition(ListNode head, int x) {
    if(head == null || head.next == null) return head;
    ListNode node = head;
    ListNode pre = null;
    ListNode rHead = null;
    ListNode rPre = null;
    while(node != null){
        if(node.val < x){
            if(head == null) head = node;
            if(pre != null) pre.next = node;
            pre = node;
        } else {
            if(head == node) head = null;
            if(rHead == null) rHead = node;
            if(rPre != null) rPre.next = node;
            rPre = node;
        }
        node = node.next;
    }
    if(pre != null) pre.next = rHead;
    else return rHead;
    if(rPre != null) rPre.next = null;
    return head;
}
```