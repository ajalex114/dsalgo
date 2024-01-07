---
layout: post
title: LC 187. Repeated DNA Sequences
categories: [LeetCode, Sliding Window, Medium]
---

LeetCode Link: [Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/)  
Language: `C#`

## Problem Statement
The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'.

For example, "ACGAATTCCG" is a DNA sequence.
When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string s that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

## Examples

Example 1:

Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
Output: ["AAAAACCCCC","CCCCCAAAAA"]
Example 2:

Input: s = "AAAAAAAAAAAAA"
Output: ["AAAAAAAAAA"]

## Constraints

* 1 <= s.length <= 105
* s[i] is either 'A', 'C', 'G', or 'T'.

## Solution

``` csharp
public class Solution 
{
    public IList<string> FindRepeatedDnaSequences(string s) 
    {
        var result = new HashSet<string>();
        var set = new HashSet<string>();
        var ap = 0;
        var bp = 9;

        if (s.Length < 10) 
        {
            return result.ToList();
        }        

        while (bp < s.Length)
        {
            var s1 = s.Substring(ap, 10);
            if(set.Contains(s1))
            {
                result.Add(s1);
            }
            set.Add(s1);
            ap++;
            bp++;
        }

        return result.ToList();
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
