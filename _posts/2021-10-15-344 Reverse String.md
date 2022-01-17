---
layout: post
title: LC 344 Reverse String
categories: [LeetCode, String, Recursion, Easy, Amazon, Microsoft]
---

LeetCode Link: [https://leetcode.com/problems/reverse-string/](https://leetcode.com/problems/reverse-string/)  
Language: `C#`

## Problem Statement
Write a function that reverses a string. The input string is given as an array of characters s.

## Examples

Example 1:

```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

Example 2:

```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## Constraints  

* 1 <= s.length <= 105
* s[i] is a printable ascii character.
* Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

## Solution

``` csharp
public class Solution 
{
    public void ReverseString(char[] s) 
    {
        Reverse(s, 0);
    }
    
    private void Reverse(char[] s, int pos)
    {
        if (pos == s.Length)
        {
            return;
        }
        
        var c = s[pos];
        Reverse(s, pos + 1);
        s[s.Length - pos - 1] = c;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(1)`  
