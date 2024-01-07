---
layout: post
title: LC 209. Minimum Size Subarray Sum
categories: [LeetCode, Sliding Window, Medium]
---

LeetCode Link: [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)  
Language: `C#`

## Problem Statement
Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

## Examples

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
Example 2:

Input: target = 4, nums = [1,4,4]
Output: 1
Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0

## Constraints

* 1 <= target <= 109
* 1 <= nums.length <= 105
* 1 <= nums[i] <= 104

## Solution

``` csharp
public class Solution 
{
    public int MinSubArrayLen(int target, int[] nums) 
    {    
        var ap = 0;
        var bp = 0;
        var min = nums.Length + 1;
        var sum = 0;

        while(bp < nums.Length)
        {
            sum = sum + nums[bp];
            if (sum >= target)
            {
                min = Math.Min(min, bp-ap+1);
                sum = sum - nums[ap] - nums[bp];
                ap++;
            }
            else
            {
                bp++;
            }
        }

        return min <= nums.Length ? min : 0;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
