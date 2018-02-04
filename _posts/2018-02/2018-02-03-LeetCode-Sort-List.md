---
layout: post
title: LeetCode - Sort List
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Sort a linked list in O(n log n) time using constant space complexity.
<!--more-->
### Java Solution
```java
class Solution {
    public ListNode sortList(ListNode head) {
        return sortList(head, null);
    }

    private ListNode sortList(ListNode head, ListNode tail){
        if(head.next == tail) return head;
        ListNode newHead = null;
        ListNode pre = null;
        ListNode node = head;
        int temp = head.val;
        System.out.println(head== null ? "null":head.val + "|" + (tail == null ? "null" : tail.val));
        while(node.next != tail){
            if(node.next.val < temp){
                if(newHead == null) newHead = node.next;
                if(pre != null) pre.next = node.next;
                pre = node.next;
            }
            node = node.next;
        }
        if(newHead != null){
            pre.next = head;
            newHead = sortList(newHead, head);
            head.next = sortList(head.next, tail);
            return newHead;
        }

        head.next = sortList(head.next, tail);
        return head;
    }
}
```