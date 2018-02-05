---
layout: post
title: LeetCode - Add Two Numbers
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
<!--more-->
**Example**
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
### Java Solution
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    boolean acc = false;
    ListNode head = null;
    ListNode pre = null;
    while(l1 != null && l2 != null){
        int sum = l2.val + l1.val;
        if(acc) sum++;
        if(sum >= 10) acc = true;
        else acc = false;
        ListNode node = new ListNode(sum % 10);
        if(head == null) head = node;
        if(pre != null) pre.next = node;
        pre = node;
        l1 = l1.next;
        l2 = l2.next;
    }
    while(l1 != null){
        int sum = l1.val;
        if(acc) sum++;
        if(sum >= 10) acc = true;
        else acc = false;
        ListNode node = new ListNode(sum % 10);
        if(head == null) head = node;
        if(pre != null) pre.next = node;
        pre = node;
        l1 = l1.next;
    }
    while(l2 != null){
        int sum = l2.val;
        if(acc) sum++;
        if(sum >= 10) acc = true;
        else acc = false;
        ListNode node = new ListNode(sum % 10);
        if(head == null) head = node;
        if(pre != null) pre.next = node;
        pre = node;
        l2 = l2.next;
    }
    if(acc) {
        ListNode node = new ListNode(1);
        pre.next = node;
    };
    return head;
}
```