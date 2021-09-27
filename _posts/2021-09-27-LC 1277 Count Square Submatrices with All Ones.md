---
layout: post
title: LC 1277 Count Square Submatrices with All Ones
categories: [LeetCode, Array, 2D, Medium, G, M, A]
---

LeetCode Link: [https://leetcode.com/problems/count-square-submatrices-with-all-ones/](https://leetcode.com/problems/count-square-submatrices-with-all-ones/)  
Language: `C#`

# Problem Statement #

Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.

## Examples

Example 1:

```
Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
Explanation: 
There are 10 squares of side 1.
There are 4 squares of side 2.
There is  1 square of side 3.
Total number of squares = 10 + 4 + 1 = 15.
```

Example 2:

```
Input: matrix = 
[
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
Explanation: 
There are 6 squares of side 1.  
There is 1 square of side 2. 
Total number of squares = 6 + 1 = 7.

```
## Constraints  

* 1 <= arr.length <= 300
* 1 <= arr[0].length <= 300
* 0 <= arr[i][j] <= 1

# Solution

``` csharp
public class Solution 
{
    public int CountSquares(int[][] matrix) => GetNoOfSquares(matrix);        
    
    private int GetNoOfSquares(int[][] matrix)
    {
        int noOfSquares = 0;
        var x = matrix.Length;
        var y = matrix[0].Length;
        
        for (int i=0; i<x; i++)
        {            
            for (int j=0; j<y; j++)
            {
                if (matrix[i][j] == 1)
                {
                    if (i!=0 && j!=0 && matrix[i-1][j] > 0 && matrix[i][j-1] > 0 && matrix[i-1][j-1] > 0)
                    {                        
                        matrix[i][j] = Min(matrix[i-1][j-1], matrix[i-1][j], matrix[i][j-1]) + 1;
                    }
                    
                    noOfSquares += matrix[i][j];
                }
            }
        }
        
        return noOfSquares;
    }
    
    private int Min(params int[] values)
    {
        int min = int.MaxValue;
        
        foreach (var item in values)
        {
            if (item < min)
            {
                min = item;
            }
        }
        
        return min;
    }
}
```

## Complexities

**Time Complexity**: `O(m*n)`  
**Space Complexity**: `O(1)`
