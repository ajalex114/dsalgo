---
layout: post
title: LC 56 Merge Intervals
categories: [LeetCode, Array, Medium, Amazon, Microsoft, Facebook, Google, Uber, Apple, LinkedIn]
---

LeetCode Link: [https://leetcode.com/problems/merge-intervals/](https://leetcode.com/problems/merge-intervals/)  
Language: `C#`

## Problem Statement

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

## Examples

Example 1:

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

Example 2:

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

## Constraints  

* 1 <= intervals.length <= 104
* intervals[i].length == 2
* 0 <= starti <= endi <= 104

## Solution

``` csharp
public class Solution 
{
    public int[][] Merge(int[][] intervals) 
    {
        var intvls = intervals.OrderBy(x=>x[0]).ToArray();
       return MergeOverlaps(intvls);
    }
    
    private int[][] MergeOverlaps(int[][] intvls)
    {
        var list = new List<int[]>();
        var len = intvls.Length;
        int start = -1;
        int end = -1;

        for (int i=0; i<len; i++)
        {
            if (start == -1)
            {
                start = intvls[i][0];
            }
            
            if (end < intvls[i][1])
            {            
                end = intvls[i][1];
            }
            
            if (i+1 < len && end >= intvls[i+1][0])
            {
                continue;
            }
            
            list.Add(new[] {start, end});
            
            start = -1;
            end = -1;
        }
        
        return list.ToArray();    
    }
}
```

## Complexity

Time Complexity: `O(NLogN)`  
Space Complexity: `O(N)`  
_If `Array.Sort` was performed instead of `OrderBy`, Space Complexity would have been `O(1)`_
