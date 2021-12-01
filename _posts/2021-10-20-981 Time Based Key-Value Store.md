---
layout: post
title: LC 981 Time Based Key-Value Store
categories: [LeetCode, HashMap, Medium, Google, Microsoft, Amazon, Apple, Netflix, Oracle]
---

LeetCode Link: [https://leetcode.com/problems/time-based-key-value-store/](https://leetcode.com/problems/time-based-key-value-store/)  
Language: `C#`

## Problem Statement
Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the TimeMap class:

TimeMap() Initializes the object of the data structure.
void set(String key, String value, int timestamp) Stores the key key with the value value at the given time timestamp.
String get(String key, int timestamp) Returns a value such that set was called previously, with timestamp_prev <= timestamp. If there are multiple such values, it returns the value associated with the largest timestamp_prev. If there are no values, it returns "".

## Examples

Example 1:

```
Input
["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
Output
[null, null, "bar", "bar", null, "bar2", "bar2"]

Explanation
TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);  // store the key "foo" and value "bar" along with timestamp = 1.
timeMap.get("foo", 1);         // return "bar"
timeMap.get("foo", 3);         // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".
timeMap.set("foo", "bar2", 4); // store the key "foo" and value "ba2r" along with timestamp = 4.
timeMap.get("foo", 4);         // return "bar2"
timeMap.get("foo", 5);         // return "bar2"
```

## Constraints  

* 1 <= key.length, value.length <= 100
* key and value consist of lowercase English letters and digits.
* 1 <= timestamp <= 107
* All the timestamps timestamp of set are strictly increasing.
* At most 2 * 105 calls will be made to set and get.

## Solution

``` csharp
public class TimeMap 
{
    private readonly Dictionary<string, Dictionary<string, string>> dict;
    
    public TimeMap() 
    {
        dict = new Dictionary<string, Dictionary<string, string>>();
    }
    
    public void Set(string key, string value, int timestamp) 
    {
        var newKey = $"{key}{timestamp}";
        
        if(!dict.ContainsKey(key))
        {
            dict[key] = new Dictionary<string, string>();            
        }
        
        dict[key][newKey] = value;        
    }
    
    public string Get(string key, int timestamp) 
    {        
        if (!dict.ContainsKey(key))
        {
            return "";
        }

        var d = dict[key];
        
        var newKey = $"{key}{timestamp}";
        while (!d.ContainsKey(newKey) && timestamp > 0)
        {
            timestamp--;
            newKey = $"{key}{timestamp}";            
        }
        
        return d.ContainsKey(newKey) ? d[newKey] : "";
    }
}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.Set(key,value,timestamp);
 * string param_2 = obj.Get(key,timestamp);
 */
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
