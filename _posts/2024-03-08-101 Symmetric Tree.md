---
layout: post
title: LC 101 Symmetric Tree
categories: [LeetCode, Tree, Easy, Microsoft, Amazon, Google]
---

LeetCode Link: [101 Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)  
Language: `C#`  

## Problem Statement
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

## Examples

Example 1:

![img1](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)
Input: root = [1,2,2,3,4,4,3]
Output: true

Example 2:

![img1](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)
Input: root = [1,2,2,null,3,null,3]
Output: false
 
## Constraints  

* The number of nodes in the tree is in the range [1, 1000].
* -100 <= Node.val <= 100

## Solution

``` csharp
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution 
{
    public bool IsSymmetric(TreeNode root) 
    {
        if (root is null)
        {
            return true;
        }

        return Sym(root.left, root.right);
    }

    private bool Sym(TreeNode l, TreeNode r)
    {
        if (l is null && r is null)
        {
            return true;
        }

        if (l is null || r is null)
        {
            return false;
        }

        if (l.val != r.val)
        {
            return false;
        }

        return Sym(l.left, r.right) && Sym(l.right, r.left);
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
