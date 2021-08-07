---
layout: post
title: LC 17 Letter Combinations of a Phone Number
categories: [LeetCode, recursion, Medium]
---

LeetCode Link: https://leetcode.com/problems/letter-combinations-of-a-phone-number/  
Language: `C#`

# Problem Statement #

```
Given a string containing digits from 2-9 inclusive,  
return all possible letter combinations that the number could represent. 
Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below.  
Note that 1 does not map to any letters.
```

## Example 1:

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

## Example 2:
```
Input: digits = ""
Output: []
```
## Example 3:
```
Input: digits = "2"
Output: ["a","b","c"]
```

## Constraints  

* 0 <= digits.length <= 4
* digits[i] is a digit in the range ['2', '9'].

# Solution

``` csharp
public class Solution 
{
    public IList<string> LetterCombinations(string digits) 
    {

        var list = new List<string>();
        var sb = new StringBuilder(digits.Length);
        var result = new List<string>();

        if(digits.Length > 0)
        {
            foreach (char c in digits)
            {
                list.Add(GetCharsForDigit(c));
                sb.Append(" ");
            }   

            GetCombinations(list, result, sb, 0);        
        }

        return result;
    }
    
    private void GetCombinations(List<string> list, List<string> result, StringBuilder sb, int pos) 
    {
        if (pos == list.Count)
        {
            result.Add(sb.ToString());
            return;
        }
        
        foreach (var c in list[pos])
        {
            sb.Remove(pos,1);
            sb.Insert(pos, c);                
            GetCombinations(list, result, sb, pos+1);            
        }
    }
    
    private string GetCharsForDigit(char c)
    {
        var list = new Dictionary<char,string>()
        {
            { '1', ""     },
            { '2', "abc"  },
            { '3', "def"  },
            { '4', "ghi"  },
            { '5', "jkl"  },
            { '6', "mno"  },
            { '7', "pqrs" },
            { '8', "tuv"  },
            { '9', "wxyz" },
            { '0', ""     }
        };
        
        return list[c];
    }
}
```

_Time Complexity: `O(m^n)` where m is the number of digits and n is the number of characters_  

