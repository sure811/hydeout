---
layout: post
title: LeetCode - Reverse Linked List II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

**Note:**

Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.
### Java Solution
```java
public ListNode reverseBetween(ListNode head, int m, int n) {
    ListNode dummy = new ListNode(-1);
    dummy.next = head;
    ListNode cur = dummy;
    ListNode pre = null;
    ListNode front = null;
    ListNode last = null;
    for (int i = 1; i <= m - 1; ++i) cur = cur.next;
    pre = cur;
    last = cur.next;
    for (int i = m; i <= n; ++i) {
        cur = pre.next;
        pre.next = cur.next;
        cur.next = front;
        front = cur;
    }
    cur = pre.next;
    pre.next = front;
    last.next = cur;
    return dummy.next;
}
```