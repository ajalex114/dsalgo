---
layout: post
title: LC 1509 Minimum Difference Between Largest and Smallest Value in Three Moves
categories: [LeetCode, Array, Medium, G]
---

LeetCode Link: [https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/](https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/)  
Language: `C#`

## Problem Statement

Given an array nums, you are allowed to choose one element of nums and change it by any value in one move.

Return the minimum difference between the largest and smallest value of nums after perfoming at most 3 moves.

## Examples

Example 1:

```
Input: nums = [5,3,2,4]
Output: 0
Explanation: Change the array [5,3,2,4] to [2,2,2,2].
The difference between the maximum and minimum is 2-2 = 0.
```

Example 2:

```
Input: nums = [1,5,0,10,14]
Output: 1
Explanation: Change the array [1,5,0,10,14] to [1,1,0,1,1]. 
The difference between the maximum and minimum is 1-0 = 1.
```

Example 3:

```
Input: nums = [6,6,0,1,1,4,6]
Output: 2
```

Example 4:

```
Input: nums = [1,5,6,14,15]
Output: 1
```

## Constraints  

* 1 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

## Solution

``` csharp
public class Solution 
{
    public int MinDifference(int[] nums) 
    {        
        if(nums.Length <= 4)
            return 0;
        
        var l = nums.Length;
        Array.Sort(nums);

        return Min(nums[l-4] - nums[0], 
                    nums[l-3] - nums[1], 
                    nums[l-2] - nums[2], 
                    nums[l-1] - nums[3]);
    }
    
    private int Min(params int[] diffs)
    {
        int min = int.MaxValue;
        
        foreach (var d in diffs)
        {
            if (d < min)
            {
                min = d;
            }
        }
        
        return min;
    }
}
```

## Notes

This one's a bit tricky.  
Basically what you have to understand is that the best option is to replace the first four items with the first item or the last 4 item with the last but the 4th item.  
But, there could also be other scenarios which is a better answer.  
### eg:  
```
[82,81,95,75,20]
```

### Sort it:  
```
Index: 0  1  2  3  4  5
Array: 20 75 81 82 95
```

### The possible outcomes are:  
```
Index: 0  1  2  3  4  5
       20 20 20 20 95
       20 75 75 75 75
       75 75 81 81 81
       81 81 81 82 82
       82 82 82 82 95
```

If you look closer, we are replacing a combination of items from beginning and ending which total 3 items.

### Option 1:

smallest : `arr[0]`  
largest: last but 4th: `arr[n-4]`
now the diff is: `arr[n-4] - arr[0]`

### Option 2:  

Replace 0th element with 1st element.  
Replace the rest at the end.  

smallest : `arr[1]`  
largest: last but 4th: `arr[n-3]`
now the diff is: `arr[n-3] - arr[1]`

### Option 3:

Replace 0th element and 1st element with 2nd element.  
Replace the rest at the end.  

smallest : `arr[2]`  
largest: last but 4th: `arr[n-2]`
now the diff is: `arr[n-2] - arr[2]`

### Option 4:

Replace 0th element and 1st and 2nd element with 3nd element.  
Replace nothing at the end.  

smallest : `arr[3]`  
largest: last but 4th: `arr[n-1]`
now the diff is: `arr[n-1] - arr[3]`

The correct answer could be any of them, or basically the minimum of it.

Hence, the answer is:  

```
 Min(nums[l-4] - nums[0], 
     nums[l-3] - nums[1], 
     nums[l-2] - nums[2], 
     nums[l-1] - nums[3]);
```