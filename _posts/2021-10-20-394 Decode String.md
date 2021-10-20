---
layout: post
title: LC 394 Decode String
categories: [LeetCode, Stack, Medium, G, M, U, A, F, O]
---

LeetCode Link: [https://leetcode.com/problems/decode-string/](https://leetcode.com/problems/decode-string/)  
Language: `C#`

## Problem Statement
Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

## Examples

Example 1:

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```

Example 2:

```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```

Example 3:

```
Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

Example 4:

```
Input: s = "abc3[cd]xyz"
Output: "abccdcdcdxyz"
```

## Constraints  

* 1 <= s.length <= 30
* s consists of lowercase English letters, digits, and square brackets '[]'.
* s is guaranteed to be a valid input.
* All the integers in s are in the range [1, 300].

## Solution

``` csharp
public class Solution 
{
    public string DecodeString(string s) 
    {     
        var sn = new Stack<int>();
        var ss = new Stack<string>();
        var temp = "";
        int i=0;
        
        while (i < s.Length)
        {
            if (int.TryParse(s[i].ToString(), out _))
            {
                int count = 0;
                while (int.TryParse(s[i].ToString(), out var c))
                {
                    count *= 10;
                    count += c;
                    i++;
                }
                sn.Push(count);
            }
            else if (s[i] == '[')
            {
                ss.Push(temp);
                temp = "";
                i++;
            }
            else if (s[i] == ']')
            {
                var count = sn.Pop();
                var existing = new StringBuilder(ss.Pop());
                
                for (int j=0; j<count; j++)
                {
                    existing.Append(temp);
                }
                
                temp = existing.ToString();
                i++;
            }
            else 
            {
                temp += s[i];
                i++;
            }
        }        
        
        return temp;
    }    
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
