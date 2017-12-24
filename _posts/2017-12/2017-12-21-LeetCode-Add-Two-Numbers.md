---
layout: post
title: LeetCode - Add Two Numbers
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Math
excerpt_separator: "<!--more-->"
---

### Question Definition

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
<!--more-->

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
### Java Solution
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if(l1 == null) return l2;
    if(l2 == null) return l1;

    ListNode head = null;
    ListNode tail = null;
    boolean acc = false;
    while(l1 != null && l2 != null){
        System.out.println(l1.val + ":" + l2.val);
        int val = l1.val + l2.val;
        if(acc)
            val++;
        if(val > 9){
            acc = true;
            val = val % 10;
        }else
            acc = false;

        ListNode temp = new ListNode(val);
        if(head == null){
            head = temp;
            tail = temp;
        }
        else{
            tail.next = temp;
            tail = temp;
        }
        l1 = l1.next;
        l2 = l2.next;
    }
    while(l1 != null){
        int val = l1.val;
        if(acc)
            val++;
        if(val > 9){
            acc = true;
            val = val % 10;
        }else
            acc = false;
        ListNode temp = new ListNode(val);
        if(head == null){
            head = temp;
            tail = temp;
        }
        else{
            tail.next = temp;
            tail = temp;
        }
        l1 = l1.next;
    }

    while(l2 != null){
        int val = l2.val;
        if(acc)
            val++;
        if(val > 9){
            acc = true;
            val = val % 10;
        }else
            acc = false;
        ListNode temp = new ListNode(val);
        if(head == null){
            head = temp;
            tail = temp;
        }
        else{
            tail.next = temp;
            tail = temp;
        }
        l2 = l2.next;
    }
    if(acc){
        ListNode temp = new ListNode(1);
        tail.next = temp;
    }
    return head;
}
```