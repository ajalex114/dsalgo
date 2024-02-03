---
layout: post
title: LC 49. Group Anagrams
categories: [LeetCode, Array, Medium, String, Microsoft, Google, Amazon]
---

LeetCode Link: [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)  
Language: `C#`  

## Problem Statement

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Examples

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Example 2:

Input: strs = [""]
Output: [[""]]
Example 3:

Input: strs = ["a"]
Output: [["a"]]

## Constraints  

* 1 <= strs.length <= 104
* 0 <= strs[i].length <= 100
* strs[i] consists of lowercase English letters.

## Solution

``` csharp
public class Solution 
{
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        var dict = new Dictionary<string, List<int>>();
        var result = new List<IList<string>>();

        for (int i=0; i<strs.Length; i++)
        {
            var s = strs[i];
            var ch = s.ToCharArray();
            Array.Sort(ch);
            var o = new string(ch);

            if (!dict.ContainsKey(o))
            {
                dict[o] = new List<int>();
            }

            dict[o].Add(i);
        }

        foreach (var d in dict.Keys)
        {
            var list = new List<string>();

            foreach (var index in dict[d])
            {
                list.Add(strs[index]);
            }

            result.Add(list);
        }

        return result;    
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
