---
layout: post
title:  Add Two Numbers
author: Zhen Zhao
date:   2015-07-01 11:45:43 -05:00
categories: LinkedList
---
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input:** (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output:** 7 -> 0 -> 8

### Clarify:
1. Store result in which LinkedList or create a new one?

### Solution:
{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null || l2 == null)
            return l1 == null? l2: l1;
        ListNode newHead = new ListNode(0);
        newHead.next = l1;
        ListNode pre = newHead;
        int carry = 0;
        while(l1 != null && l2 != null) {
            int temp = l1.val + l2.val + carry;
            l1.val = temp%10;
            carry = temp/10;
            l1 = l1.next;
            l2 = l2.next;
            pre = pre.next;
        }
        if(l2 != null) {
            pre.next = l2;
            l1 = pre.next;
        }
        while(l1!= null ){
            if(carry != 0) {
                int temp = l1.val + carry;
                l1.val = temp%10;
                carry = temp/10;
                pre = pre.next;
            }
            else
                break;
            l1 = l1.next;
        }
        // do not forget when both are null, carry = 1.
        if(carry != 0){
            pre.next = new ListNode(1);
        }
        return newHead.next;
    }
}
{% endhighlight %}