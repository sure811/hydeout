---
layout: post
title: LeetCode - Odd Even Linked List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.
<!--more-->

**Example:**

Given 1->2->3->4->5->NULL,
return 1->3->5->2->4->NULL.

**Note:**

The relative order inside both the even and odd groups should remain as it was in the input.
The first node is considered odd, the second node even and so on ...
### Java Solution
```java
public ListNode oddEvenList(ListNode head) {
    if(head == null || head.next == null || head.next.next == null) return head;
    ListNode evenHead = head;
    ListNode oddHead = head.next;
    ListNode evenPre = head;
    ListNode oddPre = head.next;
    boolean odd = false;
    head = head.next.next;
    while(head != null){
        if(odd){
            oddPre.next = head;
            oddPre = head;
        }else{
            evenPre.next = head;
            evenPre = head;
        }
        head = head.next;
        odd = !odd;
    }
    evenPre.next = oddHead;
    oddPre.next = null;
    return evenHead;
}
```