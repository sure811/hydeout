---
layout: post
title: LeetCode - Remove Duplicates from Sorted List II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.
<!--more-->

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
### Java Solution
```java
public ListNode deleteDuplicates(ListNode head) {
    if(head == null || head.next == null) return head;
    ListNode node = head;
    ListNode pre = null;
    while(node != null){
        if(node.next != null && node.val == node.next.val){
            if(node == head) head = null;
            while(node.next != null && node.val == node.next.val)
                node = node.next;
        }else{
            if(head == null) head = node;
            if(pre != null) pre.next = node;
            pre = node;
        }
        node = node.next;
    }
    if(pre != null)
        pre.next = null;
    return head;
}
```