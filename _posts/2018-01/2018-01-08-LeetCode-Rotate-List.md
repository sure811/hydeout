---
layout: post
title: LeetCode - Rotate List
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Two Pointers
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a list, rotate the list to the right by k places, where k is non-negative.


Example:
```
Given 1->2->3->4->5->NULL and k = 2,

return 4->5->1->2->3->NULL.
```
### Java Solution
```java
public ListNode rotateRight(ListNode head, int k) {
    if(head == null || k == 0 || head.next == null) return head;
    ListNode slow = head;
    int length = 0;
    while(slow != null){
        length++;
        slow = slow.next;
    }
    k = k % length;
    if(k == 0) return head;
    k = length - k;
    slow = head;
    while(--k > 0){
        slow = slow.next;
    }
    ListNode fast = slow.next;
    while(fast.next != null)
        fast = fast.next;
    fast.next = head;
    head = slow.next;
    slow.next = null;
    return head;
}
```