---
layout: post
title: LC 700 Search in a Binary Search Tree
categories: [LeetCode, Tree, BST, Easy, U]
---

LeetCode Link: [https://leetcode.com/problems/search-in-a-binary-search-tree/](https://leetcode.com/problems/search-in-a-binary-search-tree/)  
Language: `C#`

## Problem Statement
You are given the root of a binary search tree (BST) and an integer val.

Find the node in the BST that the node's value equals val and return the subtree rooted with that node. If such a node does not exist, return null.

## Examples

Example 1:

![Image1](https://assets.leetcode.com/uploads/2021/01/12/tree1.jpg)
```
Input: root = [4,2,7,1,3], val = 2
Output: [2,1,3]
```

Example 2:

![Image2](https://assets.leetcode.com/uploads/2021/01/12/tree2.jpg)
```
Input: root = [4,2,7,1,3], val = 5
Output: []
```

## Constraints  

* The number of nodes in the tree is in the range [1, 5000].
* 1 <= Node.val <= 107
* root is a binary search tree.
* 1 <= val <= 107

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
    public TreeNode SearchBST(TreeNode root, int val) 
    {        
        var node = root;
        
        while(node != null && node.val != val) 
        {
            if(val > node.val) 
            {
                node = node.right;
            } 
            else 
            {
                node = node.left;
            }
        }
        
        return node;        
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
