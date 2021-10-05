---
layout: post
title: LC 151. Reverse Words in a String
categories: [LeetCode, String, Medium]
---

LeetCode Link: https://leetcode.com/problems/reverse-words-in-a-string/  
Language: `C#`

## Problem Statement

Given an input string s, reverse the order of the `words`.

A `word` is defined as a sequence of non-space characters.  
The words in `s` will be separated by at least one space.

Return a string of the `words` in reverse order concatenated by a single space.

`Note` that `s` may contain leading or trailing spaces or multiple spaces between two words.  
The returned string should only have a single space separating the words.  
Do not include any extra spaces.

## Example 1:

```
Input: s = "the sky is blue"
Output: "blue is sky the"
```

## Example 2:
```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

## Example 3:
```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

## Example 4:
```
Input: s = "  Bob    Loves  Alice   "
Output: "Alice Loves Bob"
```

## Example 5:
```
Input: s = "Alice does not even like bob"
Output: "bob like even not does Alice"
```

## Constraints  

* 1 <= s.length <= 104
* s contains English letters (upper-case and lower-case), digits, and spaces ' '.
* There is at least one word in s.

## Solution

``` csharp
public class Solution 
{
    public string ReverseWords(string s) 
    {      
        int start = 0;
        int pos = s.Length - 1;
        
        while (s[start] == ' ')
            start++;
        
        while (s[pos] == ' ')
            pos--;
        
        int len = 0;       
        var sb = new StringBuilder(s.Length);
        
        while (pos >= start)
        {
            len = 0;
            
            while(pos>=start && s[pos] != ' ')
            {
                pos--;
                len++;
            }
            
            if (len > 0)
            {           
                for (int i=0; i<=len; i++)
                {
                    if(pos+i>=start && s[pos+i] != ' ')
                    {
                        sb.Append(s[pos+i]);
                    }
                }

                sb.Append(' ');
            }
            pos--;
        }
            
        sb.Remove(sb.Length-1, 1);

        return sb.ToString();
    }
}
```

## Complexity 

_Time Complexity: `O(n)`_  
_Space Complexity: `O(1)`_
