---
layout: post
title: LC 22 Generate Parentheses
categories: [LeetCode, BackTracking, Medium]
---

LeetCode Link: [https://leetcode.com/problems/generate-parentheses/](https://leetcode.com/problems/generate-parentheses/)  
Language: `C#`

## Problem Statement

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
## Examples

Example 1:

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

Example 2:

```
Input: n = 1
Output: ["()"]
```

## Constraints  

* 1 <= n <= 8

## Solution

``` csharp
public class Solution 
{
    public IList<string> GenerateParenthesis(int n) 
    {
        var list = new List<string>();
        
        Backtrack(list, string.Empty, 0,0, n);
        
        return list;
    }
    
    private void Backtrack(List<string> list, string curr, 
                                    int open, int closed, int max)
    {
        if (curr.Length == max * 2)
        {
            list.Add(curr);
            return;
        }

        if (open < max)
        {
            Backtrack(list, curr + "(", open + 1, closed, max);
        }
        
        if (closed < open)
        {
            Backtrack(list, curr + ")", open, closed + 1, max);
        }
    }
}
```
