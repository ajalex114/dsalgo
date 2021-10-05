---
layout: post
title: LC 2 Add Two Numbers
categories: [LeetCode, Linked List, Medium]
---

LeetCode Link: https://leetcode.com/problems/add-two-numbers/  
Language: `C#`

## Problem Statement

> You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.  
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Examples
```
Example 1:

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

```
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
```

```
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
``` 

## Constraints  

>The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.  

## Solution

``` csharp
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode AddTwoNumbers(ListNode l1, ListNode l2) {
        
        ListNode lt1 = l1;
        
        ListNode lt2 = l2;
        
        ListNode sum = new ListNode();
        ListNode st = null;
        int rem = 0;
        
        while (lt1 != null || lt2 != null) {
            
            if(st == null) {
                st = sum;
            }
            else {
                st.next = new ListNode();
                st = st.next;
            }
            
            st.val += rem;
            rem = 0;
            
            if(lt1 != null) {
                st.val += lt1.val;
                lt1 = lt1.next;
            }
            
            if(lt2 != null) {
                st.val += lt2.val;  
                lt2 = lt2.next;
            }            
            
            if(st.val > 9) {
                rem = 1;
                st.val -= 10;
            }  
            
            Console.WriteLine(st.val);
        }
        
        if(rem != 0) {
            st.next = new ListNode(rem);
        }
        
        return sum;
    }
}
```
