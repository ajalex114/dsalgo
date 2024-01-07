---
layout: post
title: LC 3 Longest Substring without repeating characters
categories: [LeetCode, Sliding Window, Medium]
---

LeetCode Link: [Longest Substring without repeating characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)  
Language: `C#`

## Problem Statement
Given a string s, find the length of the longest 
substring
 without repeating characters.

## Examples

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Constraints

* 0 <= s.length <= 5 * 104
* s consists of English letters, digits, symbols and spaces.

## Solution

``` csharp
public class Solution 
{
    public int LengthOfLongestSubstring(string s) 
    {
        var d = new HashSet<char>();
        var max = 1;
        var ap = 0;
        var bp = 0;
        int count = 0;
        
        if (s.Length < 2)
        {
            return s.Length;
        }

        while (bp < s.Length)
        {
            if(!d.Contains(s[bp]))
            {                
                d.Add(s[bp]);
                max = Math.Max(max, bp-ap+1);
                bp++;
                continue;
            }
            d.Remove(s[ap]);
            ap++;
        }
        return max;
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
