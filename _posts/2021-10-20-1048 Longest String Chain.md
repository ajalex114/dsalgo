---
layout: post
title: LC 1048 Longest String Chain
categories: [LeetCode, String, DP, Medium, Google]
---

LeetCode Link: [https://leetcode.com/problems/longest-string-chain/](https://leetcode.com/problems/longest-string-chain/)  
Language: `C#`

## Problem Statement
You are given an array of words where each word consists of lowercase English letters.

wordA is a predecessor of wordB if and only if we can insert exactly one letter anywhere in wordA without changing the order of the other characters to make it equal to wordB.

For example, "abc" is a predecessor of "abac", while "cba" is not a predecessor of "bcad".
A word chain is a sequence of words [word1, word2, ..., wordk] with k >= 1, where word1 is a predecessor of word2, word2 is a predecessor of word3, and so on. A single word is trivially a word chain with k == 1.

Return the length of the longest possible word chain with words chosen from the given list of words.

## Examples

Example 1:

```
Input: words = ["a","b","ba","bca","bda","bdca"]
Output: 4
Explanation: One of the longest word chains is ["a","ba","bda","bdca"].
```

Example 2:

```
Input: words = ["xbc","pcxbcf","xb","cxbc","pcxbc"]
Output: 5
Explanation: All the words can be put in a word chain ["xb", "xbc", "cxbc", "pcxbc", "pcxbcf"].
```

Example 3:

```
Input: words = ["abcd","dbqca"]
Output: 1
Explanation: The trivial word chain ["abcd"] is one of the longest word chains.
["abcd","dbqca"] is not a valid word chain because the ordering of the letters is changed.
```

## Constraints  

* 1 <= words.length <= 1000
* 1 <= words[i].length <= 16
* words[i] only consists of lowercase English letters.

## Solution

``` csharp
public class Solution 
{
    Dictionary<string, int> wordChain = new Dictionary<string, int>();
    Dictionary<int, HashSet<string>> dict = new Dictionary<int, HashSet<string>>();
    
    public int LongestStrChain(string[] words) 
    {
        var set = new HashSet<string>(words);        
        int max = 1;
        var maxLen = set.OrderByDescending(x=>x.Length).First().Length;

        foreach(var word in set.OrderByDescending(x=>x.Length))
        {        
            var len = word.Length;
            var val = 1;
            wordChain[word] = 1;
            
            if(!dict.ContainsKey(len))
            {
                dict[len] = new HashSet<string>();
            }
            dict[len].Add(word);
            
            if (word.Length == maxLen)
            {
                continue;
            }            
            if (!dict.ContainsKey(word.Length + 1))
            {
                continue;
            }
            
            for (int l=0; l<=word.Length; l++)
            {
                foreach(var sub in dict[word.Length + 1])
                {
                    var first = sub.Substring(0,l);                    
                    var second = sub.Substring(l+1);                    
                    var word1 = word.Substring(0,l);
                    var word2 = word.Substring(l);

                    if (word1 == first && word2 == second)
                    {
                        if (wordChain[word] <= wordChain[sub])
                        {
                            wordChain[word] = wordChain[sub] + 1;
                        }
                    }
                }
            }
            if (wordChain[word] > max)
            {
                max = wordChain[word];
            }
        }
        
        return max;                
    }    
}
```

## Complexity

Time Complexity: `O(N*L)`  
Space Complexity: `O(N)`  
