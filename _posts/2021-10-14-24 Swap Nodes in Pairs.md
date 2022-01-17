---
layout: post
title: LC 24 Swap Nodes in Pairs
categories: [LeetCode, LinkedList, Medium, Amazon, Microsoft, Facebook, Google]
---

LeetCode Link: [https://leetcode.com/problems/swap-nodes-in-pairs/](https://leetcode.com/problems/swap-nodes-in-pairs/)  
Language: `C#`

## Problem Statement

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

## Examples

Example 1:

![Example Image](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)
```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

Example 2:

```
Input: head = []
Output: []
```

Example 3:

```
Input: head = [1]
Output: [1]
```

## Constraints  

* The number of nodes in the list is in the range [0, 100].
* 0 <= Node.val <= 100

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
public class Solution 
{
    public ListNode SwapPairs(ListNode head) 
    {        
        if (head is null || head.next is null)
        {
            return head;
        }
        
        return Swap(head);        
    }
    
    private ListNode Swap(ListNode node)
    {
        var head = node.next;  
        ListNode tmp = null;
        
        while (node != null && node.next != null)
        {
            var next = node.next;            
            var nnext = next.next;
            
            node.next = nnext;
            next.next = node;
            
            if (tmp != null)
            {
                tmp.next = next;
            }

            tmp = node;
            node = node.next;
        }
        
        return head;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`
