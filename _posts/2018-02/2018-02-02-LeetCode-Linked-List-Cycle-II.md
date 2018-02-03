---
layout: post
title: LeetCode - Linked List Cycle II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
<!--more-->

**Note:**
Do not modify the linked list.

**Follow up:**

Can you solve it without using extra space?
### Java Solution
```java
public ListNode detectCycle(ListNode head) {
    if(head == null || head.next == null) return null;
    ListNode slow = head;
    ListNode fast = head;
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast) break;
    }
    if(fast == null || fast.next == null) return null;
    slow = head;
    while(fast != slow){
        slow = slow.next;
        fast = fast.next;
    }
    return fast;
}
```