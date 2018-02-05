---
layout: post
title: LeetCode - Reorder List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.
<!--more-->
For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.
### Java Solution
```java
public void reorderList(ListNode head) {
    if(head == null || head.next == null || head.next.next == null) return;
    ListNode slow = head;
    ListNode fast = head;
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
    }
    ListNode rHead = slow.next;
    ListNode pre = null;
    slow.next = null;
    while(rHead != null){
        ListNode temp = rHead.next;
        rHead.next = pre;
        pre = rHead;
        rHead = temp;
    }
    ListNode node = head;
    while(pre != null){
        ListNode rTemp = pre.next;
        ListNode temp = node.next;
        pre.next = node.next;
        node.next = pre;
        pre = rTemp;
        node = temp;
    }
    return;
}
```