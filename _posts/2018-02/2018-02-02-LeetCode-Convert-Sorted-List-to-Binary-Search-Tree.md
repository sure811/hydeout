---
layout: post
title: LeetCode - Convert Sorted List to Binary Search Tree
categories:
    - LeetCode(Second)
tags:
    - LeetCode(Second)
    - Medium
    - Linked List
excerpt_separator: "<!--more-->"
---

### Question Definition
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
<!--more-->

Example:
```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```
### My Java Solution
```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        return sortedListToBST(head, null);
    }

    public TreeNode sortedListToBST(ListNode head, ListNode tail){
        if(head == null) return null;
        if(head.next == null) return new TreeNode(head.val);
        if(head == tail) return new TreeNode(head.val);
        ListNode slow = head;
        ListNode fast = head.next;
        while(true){
            if(fast == tail || fast.next == tail || fast.next.next == tail) break;
            fast = fast.next.next;
            slow = slow.next;
        }
        TreeNode node = new TreeNode(slow.next.val);
        node.left = sortedListToBST(head, slow);
        if(slow.next != tail)
            node.right = sortedListToBST(slow.next.next, tail);
        return node;
    }
}
```

### Best Java Solution
```java
public class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if(head == null) return null;
        return toBST(head,null);
    }
    public TreeNode toBST(ListNode head, ListNode tail){
        if(head == tail) return null;

        ListNode slow = head;
        ListNode fast = head;

        while(fast != tail && fast.next != tail){
            fast = fast.next.next;
            slow = slow.next;
        }
        TreeNode thead = new TreeNode(slow.val);
        thead.left = toBST(head,slow);
        thead.right = toBST(slow.next,tail);
        return thead;
    }
}
```