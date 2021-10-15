---
layout: post
title: LC 206 Reverse Linked List
categories: [LeetCode, LinkedList, Recursion, Easy, A, M, G, F]
---

LeetCode Link: [https://leetcode.com/problems/reverse-linked-list/](https://leetcode.com/problems/reverse-linked-list/)  
Language: `C#`

## Problem Statement
Given the head of a singly linked list, reverse the list, and return the reversed list.

## Examples

Example 1:

![Example Image 1](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)
```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

Example 2:

![Example Image 2](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)
```
Input: head = [1,2]
Output: [2,1]
```

Example 3:

```
Input: head = []
Output: []
```

## Constraints  

* The number of nodes in the list is the range [0, 5000].
* -5000 <= Node.val <= 5000

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
    public ListNode ReverseList(ListNode head) 
    {
        return Reverse(head);
    }
    
    private ListNode Reverse(ListNode node)
    {
        if (node is null)
        {
            return null;
        }
        
        if (node.next is null)
        {
            return node;
        }
        
        var next = node.next;        
        var res = Reverse(next);
        
        node.next = null;        
        next.next = node;
        
        return res;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
