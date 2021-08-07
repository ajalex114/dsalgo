---
layout: post
title: LC 11 Container With Most Water
categories: [LeetCode, Array, Medium]
---

LeetCode Link: https://leetcode.com/problems/container-with-most-water/   
Language: `C#`

# Problem Statement #

```
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai).  

n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0).  

Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.
```

## Example 1:

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7].   
In this case, the max area of water (blue section) the container can contain is 49.
```

## Example 2:
```
Input: height = [1,1]
Output: 1
```
## Example 3:
```
Input: height = [4,3,2,1,4]
Output: 16
```
## Example 4:
```
Input: height = [1,2,1]
Output: 2 
```

## Constraints  

* n == height.length
* 2 <= n <= 105
* 0 <= height[i] <= 104

# Solution

``` csharp
public class Solution 
{
    public int MaxArea(int[] height) 
    {
        int max = 0;
        int left = 0;
        int right = height.Length - 1;
        
        while (left < right) 
        {
            int min = Math.Min(height[left], height[right]);
            int area = min * (right - left);
            
            if (area > max) {
                max = area;
            }
            
            if (height[left] < height[right]) {
                left++;
                continue;
            }
            
            right--;
        }
        
        return max;
    }
}
```

_Time Complexity: `O(n)`_  
_Space Complexity: `O(1)`_  
_Reference: [Youtube](https://www.youtube.com/watch?v=TI3e-17YAlc)_
