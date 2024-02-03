---
layout: post
title: LC 5. Longest Palindromic Substring
categories: [LeetCode, Array, Medium, String, Microsoft, Google, Amazon]
---

LeetCode Link: [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)  
Language: `C#`  

## Problem Statement
Given a string s, return the longest 
palindromic substring in s.

## Examples

Example 1:

Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
Example 2:

Input: s = "cbbd"
Output: "bb"

## Constraints  

* 1 <= s.length <= 1000
* s consist of only digits and English letters.

## Solution

``` csharp
public class Solution 
{
    public string LongestPalindrome(string s) 
    {
        if (s.Length < 2)
        {
            return s;
        }

        var start = 0;
        var end = 0;
        var palen = 1;

        for (int i=0; i<s.Length; i++)
        {
            var l1 = Palen(i, i+1, s);
            var l2 = Palen(i-1, i+1, s);
            var len = Math.Max(l1, l2);

            if (len > palen)
            {
                start = i - (len - 1)/2;
                end = i + len/2;
                palen = len;
            }
        }

        return s.Substring(start, (end - start + 1));
    }

    private int Palen(int l, int r, string s)
    {
        if (l < 0 || r >= s.Length)
        {
            return 0;
        }

        while(l >= 0 && r < s.Length && s[l] == s[r])
        {
            l--;
            r++;            
        }

        return r - l - 1;
    }
}
```

## Complexity

Time Complexity: `O(N^2)`  
Space Complexity: `O(1)`  
