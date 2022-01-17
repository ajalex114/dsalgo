---
layout: post
title: LC 366 Find Leaves of Binary Tree
categories: [LeetCode, Tree, Medium, Google, LinkedIn]
---

LeetCode Link: [https://leetcode.com/problems/find-leaves-of-binary-tree/](https://leetcode.com/problems/find-leaves-of-binary-tree/)  
Language: `C#`

## Problem Statement

Given the root of a binary tree, collect a tree's nodes as if you were doing this:

Collect all the leaf nodes.
Remove all the leaf nodes.
Repeat until the tree is empty.

![Example Image](https://assets.leetcode.com/uploads/2021/03/16/remleaves-tree.jpg)

## Examples

Example 1:

```
Input: root = [1,2,3,4,5]
Output: [[4,5,3],[2],[1]]

Explanation:

[[3,5,4],[2],[1]] and [[3,4,5],[2],[1]] are also considered correct answers since per each level it does not matter the order on which elements are returned.
```

Example 2:

```
Input: root = [1]
Output: [[1]]
```

## Constraints  

* The number of nodes in the tree is in the range [1, 100].
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
    Dictionary<int, List<int>> dict = new();
    
    public IList<IList<int>> FindLeaves(TreeNode root) 
    {        
        IList<IList<int>> list = new List<IList<int>>();
        var height = GetHeight(root);
        
        for (int i=-1; i<height; i++)
        {
            list.Add(dict[i]);
        }
        
        return list;        
    }
    
    private int GetHeight(TreeNode node)
    {
        if (node is null) return -1;
        
        var left = Post(node.left);
        var right = Post(node.right);
        
        var level = Math.Max(left, right);        
        AddToDict(level, node.val);
        
        return level + 1;
    }
    
    private void AddToDict(int level, int data)
    {
        if (!dict.ContainsKey(level))
        {
            dict[level] = new List<int>();
        }        
        dict[level].Add(data);
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`

## Notes

Utilize Hashmap for mapping the heights.  
A leaf node will have a height of -1 (or 0 based on the implementation).  
Utilize this, create a hashmap, where height is the key and the nodes at that height are the values.  
Iterate through these heights and return the list of all the list of nodes.