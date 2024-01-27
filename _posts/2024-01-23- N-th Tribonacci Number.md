---
layout: post
title: N-th Tribonacci Number
categories: [LeetCode, Array, DP, Easy]
---

LeetCode Link: [N-th Tribonacci Number]https://leetcode.com/explore/featured/card/dynamic-programming/631/strategy-for-solving-dp-problems/4041/)  
Language: `C#`

## Problem Statement
The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.

## Examples

Example 1:

Input: n = 4
Output: 4
Explanation:
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4

Example 2:

Input: n = 25
Output: 1389537

## Constraints

* 0 <= n <= 37
* The answer is guaranteed to fit within a 32-bit integer, ie. answer <= 2^31 - 1.

## Solution

``` csharp
public class Solution 
{
    public int Tribonacci(int n) 
    {
        if (n<1)
        {
            return 0;
        }
        
        if (n <= 2)
        {
            return 1;
        }

        var m = new int[3];
        m[0] = 0;
        m[1] = 1;
        m[2] = 1;
        
        for (int i=3; i<=n; i++)
        {
            var tmp = m[0] + m[1] + m[2];
            m[0] = m[1];
            m[1] = m[2];
            m[2] = tmp;
        }
        
        return m[2];
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
