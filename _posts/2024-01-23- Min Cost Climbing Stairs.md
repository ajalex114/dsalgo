---
layout: post
title: LC 219. Contains Duplicate II
categories: [LeetCode, Array, DP, Easy]
---

LeetCode Link: [Min Cost Climbing Stairs](https://leetcode.com/explore/featured/card/dynamic-programming/631/strategy-for-solving-dp-problems/4040/)  
Language: `C#`

## Problem Statement
You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.


## Examples

Example 1:

Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.

Example 2:

Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.


## Constraints

* 2 <= cost.length <= 1000
* 0 <= cost[i] <= 999

## Solution

``` csharp
public class Solution 
{
    public int MinCostClimbingStairs(int[] cost) 
    {    
        var m = new int[cost.Length];
        m[0] = cost[0];
        m[1] = cost[1];
        
        for (int i=2; i<cost.Length; i++)
        {
            m[i] = cost[i] + Math.Min(m[i-1], m[i-2]);
        }
        
        return Math.Min(m[cost.Length -1], m[cost.Length -2]);        
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
