---
layout: post
title: LeetCode - Reorder List
categories:
    - LeetCode
tags:
    - LeetCode
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
    if(head == null || head.next == null) return;
    ListNode slow = head;
    ListNode fast = head;
    ListNode pre = null;
    while(fast != null && fast.next != null){
        pre = slow;
        slow = slow.next;
        fast = fast.next.next;
    }
    pre.next = null;
    pre = null;
    while(slow != null){
        ListNode temp = slow.next;
        slow.next = pre;
        pre = slow;
        slow = temp;
    }
    ListNode cur = head;
    while(cur.next != null){
        System.out.println(pre.val);
        ListNode temp = pre.next;
        pre.next = cur.next;
        cur.next = pre;
        cur = pre.next;
        pre = temp;
    }
    cur.next = pre;
    return;
}
```