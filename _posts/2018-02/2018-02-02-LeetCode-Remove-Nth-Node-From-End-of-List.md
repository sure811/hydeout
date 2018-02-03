---
layout: post
title: LeetCode - Remove Nth Node From End of List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a linked list, remove the nth node from the end of list and return its head.
<!--more-->
For example,
```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```
**Note:**

Given n will always be valid.
Try to do this in one pass.
### Java Solution
```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode fast = head;
    while(fast != null && --n >= 0){
        fast = fast.next;
    }
    if(n == 0 && fast == null)
        return head.next;
    if(fast == null) return head;
    ListNode slow = head;
    while(fast.next != null)
    {
        slow = slow.next;
        fast = fast.next;
    }
    slow.next = slow.next.next;
    return head;
}
```