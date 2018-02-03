---
layout: post
title: LeetCode - Reverse Linked List II
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Reverse a linked list from position m to n. Do it in-place and in one-pass.
<!--more-->

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

**Note:**

Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.
### Java Solution
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if(head == null || head.next == null) return head;
        int length = n - m;
        ListNode pre = (m == 1 ? null : head);
        while(--m > 1 && pre != null) pre = pre.next;
        if(pre == null) return reverse(head, length);
        pre.next = reverse(pre.next, length);
        return head;
    }

    private ListNode reverse(ListNode head, int length){
        if(head == null || length == 0) return head;
        ListNode newHead = reverse(head.next, length - 1);
        ListNode node = newHead;
        for(int i = 0; i < length - 1 && node.next != null; i++)
            node = node.next;
        if(node != null){
            head.next = node.next;
            node.next = head;
        }

        return newHead;
    }
}
```