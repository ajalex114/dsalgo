---
layout: post
title: LC 562 Longest Line of Consecutive One in Matrix
categories: [LeetCode, Array, 2D, Medium, G]
---

LeetCode Link: [https://leetcode.com/problems/longest-line-of-consecutive-one-in-matrix/](https://leetcode.com/problems/longest-line-of-consecutive-one-in-matrix/)  
Language: `C#`

## Problem Statement

Given an m x n binary matrix mat, return the length of the longest line of consecutive one in the matrix.

The line could be horizontal, vertical, diagonal, or anti-diagonal.

## Examples

Example 1:

![Example 1](https://assets.leetcode.com/uploads/2021/04/24/long1-grid.jpg)
```
Input: mat = [[0,1,1,0],[0,1,1,0],[0,0,0,1]]
Output: 3
```

Example 2:

![Example 1](https://assets.leetcode.com/uploads/2021/04/24/long2-grid.jpg)
```
Input: mat = [[1,1,1,1],[0,1,1,0],[0,0,0,1]]
Output: 4
```

## Constraints  

* m == mat.length
* n == mat[i].length
* 1 <= m, n <= 104
* 1 <= m * n <= 104
* mat[i][j] is either 0 or 1.

## Solution

``` csharp
public class Solution 
{
    public int LongestLine(int[][] mat) 
    {        
        var copy = new int[mat.Length][][];
        int max = 0;
        
        for (int i=0; i<mat.Length; i++)
        {
            copy[i] = new int[mat[i].Length][];
            
            for(int j=0; j<mat[i].Length; j++)
            {
                copy[i][j] = new int[4];
                if (mat[i][j] == 1)
                {
                    copy[i][j][0] = 1;
                    copy[i][j][1] = 1;
                    copy[i][j][2] = 1;
                    copy[i][j][3] = 1;
                    
                    var val = SetMaxLen(copy, i, j);
                    
                    if (val > max)
                    {
                        max = val;
                    }
                }
            }
        }
        
        return max;        
    }
    
    private int SetMaxLen(int[][][] mat,int i, int j)
    {
        int max = 1;
        int val = 0;
        
        if (i-1 >= 0)
        {
            val = mat[i-1][j][0] + 1;
            mat[i][j][0] = val;
            
            if (val > max) 
            {
                max = val;
            }
        }
        if (j-1 >= 0)
        {
            val = mat[i][j-1][1] + 1;
            mat[i][j][1] = val;
            
            if (val > max) 
            {
                max = val;
            }
        }
        if (i-1 >= 0 && j-1 >= 0)
        {
            val = mat[i-1][j-1][2] + 1;
            mat[i][j][2] = val;
            
            if (val > max) 
            {
                max = val;
            }
        }
        if (i-1 >= 0 && j+1 < mat[i].Length)
        {
            val = mat[i-1][j+1][3] + 1;
            mat[i][j][3] = val;
            
            if (val > max) 
            {
                max = val;
            }
        }
        
        return max;
    }
}
```

## Complexity

Time Complexity: `O(mn)`  
Space Complexity: `O(mn)`  
