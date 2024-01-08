---
layout: post
title: LC 219. Contains Duplicate II
categories: [LeetCode, Array, Easy]
---

LeetCode Link: [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/)  
Language: `C#`

## Problem Statement
Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

## Examples

Example 1:

Input: nums = [1,2,3,1], k = 3
Output: true
Example 2:

Input: nums = [1,0,1,1], k = 1
Output: true
Example 3:

Input: nums = [1,2,3,1,2,3], k = 2
Output: false

## Constraints

* 1 <= nums.length <= 105
* -109 <= nums[i] <= 109
* 0 <= k <= 105

## Solution

``` csharp
public class Solution 
{
    public bool ContainsNearbyDuplicate(int[] nums, int k) 
    {
        var d = new Dictionary<int, int>();

        for (int i=0; i< nums.Length; i++)
        {
            if (d.ContainsKey(nums[i]))
            {
                if (i - d[nums[i]] <= k)
                {
                    return true;
                }
            }
            d[nums[i]] = i;
        }  
        return false;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
