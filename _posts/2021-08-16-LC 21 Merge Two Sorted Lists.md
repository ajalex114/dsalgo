---
layout: post
title: LC 21 Merge Two Sorted Lists
categories: [LeetCode, Linked List, Easy]
---

LeetCode Link: https://leetcode.com/problems/add-two-numbers/  
Language: `C#`

# Problem Statement #

Merge two sorted linked lists and return it as a sorted list.  
The list should be made by splicing together the nodes of the first two lists.

## Examples

Example 1:

```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

Example 2:

```
Input: l1 = [], l2 = []
Output: []
```

Example 3:

```
Input: l1 = [], l2 = [0]
Output: [0]
```  

## Constraints  

* The number of nodes in both lists is in the range [0, 50].
* -100 <= Node.val <= 100
* Both l1 and l2 are sorted in non-decreasing order.  

# Solution

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
public class Solution 
{
    private ListNode head = null;
    private ListNode tail = null;

    public ListNode MergeTwoLists(ListNode l1, ListNode l2) 
    {        
        ListNode next = null;
        
        while (l1 != null && l2 != null)
        {
            if (l1.val < l2.val)
            {
                next = l1;
                l1 = l1.next;
            }
            else
            {
                next = l2;
                l2 = l2.next;
            }
            
            AssignNext(next);
        }
        
        while (l1 != null)
        {
            AssignNext(l1);
            l1 = l1.next;
        }
        
        while (l2 != null)
        {
            AssignNext(l2); 
            l2 = l2.next;
        }        
        
        return head;
    }
    
    private void AssignNext(ListNode next)
    {
        if (head is null)
        {
            head = next;
            tail = next;
        }
        else
        {
            tail.next = next;
            tail = next;
        }          
    }
}
```
