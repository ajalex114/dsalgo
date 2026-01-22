---
layout: post
title: LC 34. Find First and Last Position of Element in Sorted Array
categories: [LeetCode, Tree, Medium, Microsoft, Amazon, Google]
---

LeetCode Link: [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)  
Language: `C#`  

## Problem Statement
Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.

## Examples

Example 1:

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
Example 2:

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
Example 3:

Input: nums = [], target = 0
Output: [-1,-1]
 
## Constraints  

* 0 <= nums.length <= 105
* -109 <= nums[i] <= 109
* nums is a non-decreasing array.
* -109 <= target <= 109

## Solution

``` csharp
public class Solution {
    public int[] SearchRange(int[] nums, int target) {
        return Search(nums, target);        
    }

    private int[] Search(int[] nums, int target)
    {
        int a = 0;
        int b = nums.Length - 1;

        while (a <= b)
        {
            int mid = (a + b)/2;
            if (nums[mid] == target)
            {
                return FetchIndeces(nums, target, mid);
            }
            if (nums[mid] > target)
            {
                b = mid - 1;
            }
            if (nums[mid] < target)
            {
                a = mid + 1;
            }
        }

        return new[] {-1,-1};
    }

    private int[] FetchIndeces(int[] nums, int target, int foundAt)
    {
        int beg = foundAt;
        int end = foundAt;
        bool begSet = false;
        bool endSet = false;

        if (foundAt == 0 || nums[foundAt - 1] != target)
        {
            beg = foundAt;
            begSet = true;
        }
        if (foundAt == nums.Length - 1 || nums[foundAt + 1] != target)
        {
            end = foundAt;
            endSet = true;
        }

        if (begSet && endSet)
        {
            return new[] {beg, end};
        }

        int a = 0;
        int b = foundAt;
        
        if (!begSet)
        {
            while (a <= b)
            {
                int newMid = (a + b)/2;

                if (nums[newMid] == target)
                {
                    beg = Math.Min(beg, newMid);
                    b = newMid - 1;
                    continue;
                }
                
                a = newMid + 1;
            }
        }

        a = foundAt;
        b = nums.Length - 1;

        if (!endSet)
        {
            while (a <= b)
            {
                int newMid = (a + b)/2;

                if (nums[newMid] == target)
                {
                    end = Math.Max(end, newMid);
                    a = newMid + 1;
                    continue;
                }
                
                b = newMid - 1;
            }
        }

        return new[] {beg, end};
    }
}
```

## Complexity

Time Complexity: `O(LogN)`  
Space Complexity: `O(1)`  
