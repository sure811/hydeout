---
layout: post
title: LeetCode - Remove Duplicates from Sorted List II
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.
<!--more-->

For example,
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
### Java Solution
```java
public ListNode deleteDuplicates(ListNode head) {
    ListNode newHead = null;
    ListNode newPre = null;
    while(head != null){
        boolean duplicate = false;
        while(head.next != null && head.next.val == head.val){
            head = head.next;
            duplicate = true;
        }

        if(!duplicate){
            ListNode newNode = new ListNode(head.val);
            if(newHead == null){
                newHead = newNode;
                newPre = newNode;
            }else{
                newPre.next = newNode;
                newPre = newNode;
            }
        }
        head = head.next;
    }
    return newHead;
}
```