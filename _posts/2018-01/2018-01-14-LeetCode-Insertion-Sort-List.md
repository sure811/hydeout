---
layout: post
title: LeetCode - Insertion Sort List
categories:
    - LeetCode
tags:
    - LeetCode
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Sort a linked list using insertion sort.
<!--more-->
### Java Solution
```java
public ListNode insertionSortList(ListNode head) {
    if(head == null) return head;
    ListNode newHead = new ListNode(head.val);
    head = head.next;
    while(head != null){
        ListNode node = new ListNode(head.val);
        if(head.val <= newHead.val){
            node.next = newHead;
            newHead = node;
            head = head.next;
            continue;
        }

        ListNode pre = newHead;
        while(pre.next != null && pre.next.val < head.val)
            pre = pre.next;
        if(pre.next == null){
            pre.next = node;
        }else{
            node.next = pre.next;
            pre.next = node;
        }
        head = head.next;
    }
    return newHead;
}
```