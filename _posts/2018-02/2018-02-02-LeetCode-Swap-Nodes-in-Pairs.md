---
layout: post
title: LeetCode - Swap Nodes in Pairs
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a linked list, swap every two adjacent nodes and return its head.
<!--more-->

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.
### Java Solution
```java
public ListNode swapPairs(ListNode head) {
    if(head == null || head.next == null) return head;
    ListNode newHead = head.next;
    ListNode pre = head;
    head = head.next;
    while(head != null){
        ListNode temp = head.next;
        head.next = pre;
        if(temp != null){
            if(temp.next == null){
                pre.next = temp;
                break;
            }else{
                pre.next = temp.next;
                pre = temp;
                head = pre.next;
            }
        } else{
            pre.next = null;
            break;
        }
    }
    return newHead;
}
```