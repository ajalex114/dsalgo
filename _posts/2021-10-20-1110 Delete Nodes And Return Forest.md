---
layout: post
title: LC 1110 Delete Nodes And Return Forest
categories: [LeetCode, Tree, Recursion, Medium, G, A, F]
---

LeetCode Link: [https://leetcode.com/problems/delete-nodes-and-return-forest/](https://leetcode.com/problems/delete-nodes-and-return-forest/)  
Language: `C#`

## Problem Statement
Given the root of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in to_delete, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

## Examples

Example 1:

![Example Image](https://assets.leetcode.com/uploads/2019/07/01/screen-shot-2019-07-01-at-53836-pm.png)
```
Input: root = [1,2,3,4,5,6,7], to_delete = [3,5]
Output: [[1,2,null,4],[6],[7]]
```


Example 1:

```
Input: root = [1,2,4,null,3], to_delete = [3]
Output: [[1,2,4]]
```

## Constraints  

* The number of nodes in the given tree is at most 1000.
* Each node has a distinct value between 1 and 1000.
* to_delete.length <= 1000
* to_delete contains distinct values between 1 and 1000.

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
    public IList<TreeNode> DelNodes(TreeNode root, int[] to_delete) 
    {
        var set = new HashSet<int>(to_delete);
        var list = new List<TreeNode>();
        
        if(!set.Contains(root.val))
        {
            list.Add(root);
        }
        
        Traverse(root, set, list, null);
        return list;
    }
    
    private void Traverse(TreeNode node, HashSet<int> toDelete, List<TreeNode> list, TreeNode parent)
    {
        if (node is null)
        {
            return;
        }
        
        if (toDelete.Contains(node.val))
        {
            if (parent != null)
            {
                if (parent.left == node)
                {
                    parent.left = null;
                }
                else
                {
                    parent.right = null;
                }
            }
            
            if (node.left != null && !toDelete.Contains(node.left.val))
            {
                list.Add(node.left);
            }
            
            if (node.right != null && !toDelete.Contains(node.right.val))
            {
                list.Add(node.right);            
            }
        }
        
        Traverse(node.left, toDelete, list, node);
        Traverse(node.right, toDelete, list, node);
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
