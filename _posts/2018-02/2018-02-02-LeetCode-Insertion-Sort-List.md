---
layout: post
title: LeetCode - Insertion Sort List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Sort a linked list using insertion sort.
<!--more-->
### Java Solution
```java
public ListNode insertionSortList(ListNode head) {
    if(head == null || head.next == null) return head;
    ListNode newHead = new ListNode(head.val);
    head = head.next;
    while(head != null){
        ListNode newNode = newHead;
        while(newNode.next != null && newNode.next.val < head.val)
            newNode = newNode.next;
        ListNode node = new ListNode(head.val);
        if(newNode == newHead && head.val < newHead.val){
            node.next = newHead;
            newHead = node;
        }else{
            node.next = newNode.next;
            newNode.next = node;
        }
        head = head.next;
    }
    return newHead;
}
```