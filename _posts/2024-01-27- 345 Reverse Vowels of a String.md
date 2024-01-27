---
layout: post
title: 345. Reverse Vowels of a String
categories: [LeetCode, Array, Easy]
---

LeetCode Link: [345. Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/?source=submission-ac)  
Language: `C#`

## Problem Statement
Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both lower and upper cases, more than once.

## Examples

Example 1:

Input: s = "hello"
Output: "holle"

Example 2:

Input: s = "leetcode"
Output: "leotcede"

## Constraints

* 1 <= s.length <= 3 * 105
* s consist of printable ASCII characters.

## Solution

``` csharp
public class Solution 
{
    public string ReverseVowels(string s) 
    {
        if (s.Length == 1)
        {
            return s;
        }   

        char[] vow = ['a','e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
        var tmp = new int[s.Length];    
        var c = 0;

        for (int i=0; i < s.Length; i++)
        {
            if (vow.Contains(s[i]))
            {
                tmp[c] = i;
                c++;
            }
        }

        if (c == 0)
        {
            return s;
        }

        var last = c-1;
        c = 0;
        
        var o = new StringBuilder();
        for (int i=0; i < s.Length; i++)
        {
            if (i == tmp[c])
            {
                o.Append(s[tmp[last]]);
                last--;
                c++;
                continue;
            }

            o.Append(s[i]);
        }

        return o.ToString();
    }

}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
