---
layout: post
title: LC 14 Longest Common Prefix
categories: [LeetCode, string, Easy]
---

LeetCode Link: https://leetcode.com/problems/longest-common-prefix/  
Language: `C#`

# Problem Statement #

```
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".
```

## Example 1:

```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

## Example 2:
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Constraints  

* 1 <= strs.length <= 200
* 0 <= strs[i].length <= 200
* strs[i] consists of only lower-case English letters.

# Solution

``` csharp
public class Solution 
{
    public string LongestCommonPrefix(string[] strs) => GetMinPrefix(strs);       
        
    private string GetMinPrefix(string[] strs)
    {
        int minPrefixSize = strs[0].Length;
        
        for (int i=1; i<strs.Length; i++)
        {
            int prefix = 0;
            
            for (int j=0; j<minPrefixSize && j<strs[i].Length; j++) 
            {
                if(strs[i-1][j] == strs[i][j]) 
                {
                    prefix++;
                }
                else
                {
                    break;
                }
            }
            
            Console.WriteLine(prefix);
            
            if (prefix == 0)
            {
                return string.Empty;
            }
            
            if (prefix < minPrefixSize)
            {
                minPrefixSize = prefix;
            }
        }
        
        return strs[0].Substring(0, minPrefixSize);
    }
}
```

_Time Complexity: `O(m*n)` where m is the number of strings and n is the length of each string_  
_Space Complexity: `O(1)`_  
