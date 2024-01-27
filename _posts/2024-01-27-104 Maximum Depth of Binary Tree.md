---
layout: post
title: 104. Maximum Depth of Binary Tree
categories: [LeetCode, Tree, BT, Easy, Recursion, Amazon, Google, Microsoft, Uber]
---

LeetCode Link: [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)  
Language: `C#`  

## Problem Statement
Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Examples

Example 1:

![Image1](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)  
Input: root = [3,9,20,null,null,15,7]
Output: 3  

Example 2:

Input: root = [1,null,2]  
Output: 2

## Constraints  

* The number of nodes in the tree is in the range [0, 104].
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
    public int MaxDepth(TreeNode root) 
    {
        if (root is null)
        {
            return 0;
        }

        var l = MaxDepth(root.left);
        var r = MaxDepth(root.right);

        return l < r ? r+1 : l+1;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
