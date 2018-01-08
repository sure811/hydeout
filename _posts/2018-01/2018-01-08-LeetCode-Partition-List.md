---
layout: post
title: LeetCode - Partition List
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Two Pointers
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
    if(head == null) return head;
    ListNode dummy = new ListNode(-1);
    ListNode newDummy = new ListNode(-1);
    dummy.next = head;
    ListNode cur = dummy, p = newDummy;
    while (cur.next != null) {
        if (cur.next.val < x) {
            p.next = cur.next;
            p = p.next;
            cur.next = cur.next.next;
            p.next = null;
        } else {
            cur = cur.next;
        }
    }
    p.next = dummy.next;
    return newDummy.next;
}
```