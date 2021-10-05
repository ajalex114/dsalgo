---
layout: post
title: LC 93 Restore IP Addresses
categories: [LeetCode, Array, Medium, G, Ap, M, A, F]
---

LeetCode Link: [https://leetcode.com/problems/restore-ip-addresses/](https://leetcode.com/problems/restore-ip-addresses/)  
Language: `C#`

## Problem Statement

Given a string s containing only digits, return all possible valid IP addresses that can be obtained from s. You can return them in any order.

A valid IP address consists of exactly four integers, each integer is between 0 and 255, separated by single dots and cannot have leading zeros. For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses and "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses. 

## Examples

Example 1:

```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```

Example 2:

```
Input: s = "0000"
Output: ["0.0.0.0"]
```

Example 3:

```
Input: s = "1111"
Output: ["1.1.1.1"]
```

Example 4:

```
Input: s = "010010"
Output: ["0.10.0.10","0.100.1.0"]
```

Example 5:

```
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

## Constraints  

* 0 <= s.length <= 3000
* s consists of digits only.

## Solution

``` csharp
public class Solution 
{
    HashSet<string> set = new HashSet<string>();
    
    public IList<string> RestoreIpAddresses(string s) 
    {
        var list = new List<string>();
        Populate(s, list, 1,1,1,1);        
        return list;
    }
    
    private void Populate(string s, List<string> list, int s1, int s2, int s3, int s4)
    {   
        if (set.Contains($"{s1}.{s2}.{s3}.{s4}"))
        {
            return;
        }        
        set.Add($"{s1}.{s2}.{s3}.{s4}");
        
        if (IsValidIpAddress(s, s1, s2, s3, s4))
        {
            var ip = FormIp(s, s1, s2, s3, s4);
            list.Add(ip);            
        }          
        
        if (s1<3 && (s1+s2+s3+s4+1) <= s.Length)
        {
            Populate(s, list, s1+1, s2, s3, s4);
        }
        if (s2<3 && (s1+s2+s3+s4+1) <= s.Length)
        {
            Populate(s, list, s1, s2+1, s3, s4);
        }
        if (s3<3 && (s1+s2+s3+s4+1) <= s.Length)
        {
            Populate(s, list, s1, s2, s3+1, s4);
        }
        if (s4<3 && (s1+s2+s3+s4+1) <= s.Length)
        {
            Populate(s, list, s1, s2, s3, s4+1);        
        }
    }
    
    private string FormIp(string s, int s1, int s2, int s3, int s4)
    {
        return string.Join(".",     
                    s.Substring(0, s1),
                    s.Substring(s1, s2),
                    s.Substring(s1+s2, s3),
                    s.Substring(s1+s2+s3, s4));
    }
    
    private bool IsValidIpAddress(string s, int s1, int s2, int s3, int s4)
    {
        if ((s1 + s2 + s3 + s4) != s.Length)
        {
            return false;
        }
        
        var items = new List<string>
        {
            s.Substring(0, s1),
            s.Substring(s1, s2),
            s.Substring(s1+s2, s3),
            s.Substring(s1+s2+s3, s4)
        };
        
        foreach (var item in items)
        {
            if (i.Length > 3)
            {
                return false;
            }
            
            int ip = 0;
            foreach (var c in item)
            {                
                ip *= 10;
                ip += GetNum(c);
            }
            
            // avoid something.010.something
            if (ip > 0 && i[0] == '0')
            {
                return false;
            }
            
            // avoid something.00.something
            if (ip==0 && i.Length > 1)
            {
                return false;
            }
            
            if (ip > 255)
            {
                return false;
            }
        }
        
        return true;
    }
    
    private int GetNum(char c)
    {
        var dict = new Dictionary<char, int>
        {
            {'1',1},
            {'2',2},
            {'3',3},
            {'4',4},
            {'5',5},
            {'6',6},
            {'7',7},
            {'8',8},
            {'9',9},
            {'0',0}
        };
        
        return dict[c];
    }
}
```

## Notes

Following backtracking mechanism.  
Have added multiple checks as part of optimization