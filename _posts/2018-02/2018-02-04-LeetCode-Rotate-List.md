---
layout: post
title: LeetCode - Rotate List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list, rotate the list to the right by k places, where k is non-negative.
<!--more-->

Example:
```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```
### Java Solution
```java
public ListNode rotateRight(ListNode head, int k) {
    if(head == null || head.next == null) return head;
    ListNode slow = head;
    int count = 0;
    while(slow != null){
        slow = slow.next;
        count++;
    }
    k = k % count;
    slow = head;
    ListNode fast = head;
    while(--k >= 0) {
        if(fast == null) fast = head;
        fast = fast.next;
    }
    while(fast != null && fast.next != null){
        slow = slow.next;
        fast = fast.next;
    }
    if(fast != null && slow != null && slow.next != null){
        ListNode rHead = head;
        head = slow.next;
        slow.next = null;
        fast.next = rHead;
    }
    return head;
}
```