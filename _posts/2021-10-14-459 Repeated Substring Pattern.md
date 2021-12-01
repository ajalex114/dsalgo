---
layout: post
title: LC 459 Repeated Substring Pattern
categories: [LeetCode, String, Easy, Google]
---

LeetCode Link: [https://leetcode.com/problems/repeated-substring-pattern/](https://leetcode.com/problems/repeated-substring-pattern/)  
Language: `C#`

## Problem Statement

Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

## Examples

Example 1:

```
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.
```

Example 2:

```
Input: s = "aba"
Output: false
```

Example 2:

```
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.
```

## Constraints  

* 1 <= s.length <= 104
* s consists of lowercase English letters.

## Solution

``` csharp
public class Solution 
{
    public bool RepeatedSubstringPattern(string s)
    {        
        var len = s.Length;        
        
        for (int i=len/2; i>0; i--)
        {
            if (len%i == 0)
            {
                int repeat = len/i;                
                string sub = s.Substring(0, i);
                string comp = "";
                
                for (int j=0; j<repeat; j++)
                {
                    comp += sub;
                }
                
                if (comp == s)
                {
                    return true;
                }
            }
        }
        
        return false;        
    }
}
```

## Complexity

Time Complexity: `O(n)`  
Space Complexity: `O(1)`  
