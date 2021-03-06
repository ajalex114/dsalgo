---
layout: post
title: LC 359 Logger Rate Limiter
categories: [LeetCode, Stream, Easy, Google]
---

LeetCode Link: [https://leetcode.com/problems/logger-rate-limiter/](https://leetcode.com/problems/logger-rate-limiter/)  
Language: `C#`

## Problem Statement

Design a logger system that receives a stream of messages along with their timestamps. Each unique message should only be printed at most every 10 seconds (i.e. a message printed at timestamp t will prevent other identical messages from being printed until timestamp t + 10).

All messages will come in chronological order. Several messages may arrive at the same timestamp.

Implement the Logger class:

Logger() Initializes the logger object.
bool shouldPrintMessage(int timestamp, string message) Returns true if the message should be printed in the given timestamp, otherwise returns false.

## Examples

Example 1:

```
Input
["Logger", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage"]
[[], [1, "foo"], [2, "bar"], [3, "foo"], [8, "bar"], [10, "foo"], [11, "foo"]]
Output
[null, true, true, false, false, false, true]

Explanation
Logger logger = new Logger();
logger.shouldPrintMessage(1, "foo");  // return true, next allowed timestamp for "foo" is 1 + 10 = 11
logger.shouldPrintMessage(2, "bar");  // return true, next allowed timestamp for "bar" is 2 + 10 = 12
logger.shouldPrintMessage(3, "foo");  // 3 < 11, return false
logger.shouldPrintMessage(8, "bar");  // 8 < 12, return false
logger.shouldPrintMessage(10, "foo"); // 10 < 11, return false
logger.shouldPrintMessage(11, "foo"); // 11 >= 11, return true, next allowed timestamp for "foo" is 11 + 10 = 21
```


## Constraints  

* 0 <= timestamp <= 109
* Every timestamp will be passed in non-decreasing order (chronological order).
* 1 <= message.length <= 30
* At most 104 calls will be made to shouldPrintMessage.

## Solution

``` csharp
public class Logger 
{   
    private readonly Dictionary<string, int> dict;

    public Logger() 
    {
        dict = new Dictionary<string, int>();
    }
    
    public bool ShouldPrintMessage(int timestamp, string message) 
    {        
        if(dict.ContainsKey(message))
        {
            if(timestamp - dict[message] >= 10)
            {
                dict[message] = timestamp;
                return true;
            }
            return false;
        }
        
        dict[message] = timestamp;
        return true;        
    }
}

/**
 * Your Logger object will be instantiated and called as such:
 * Logger obj = new Logger();
 * bool param_1 = obj.ShouldPrintMessage(timestamp,message);
 */
```

## Notes

The trick lies in understanding the question.  
Once you understand it, its fairly simple.  

Any message should not repeat inside a window of 10 seconds.

What I've done is, every message will be added to a HashTable as a key, with the value as the timestamp.

Every time a new message arrives, I'll check if it is present in the Hashtable and check if the value is more than 10 values (seconds in this case) different from the input timestamp value.
If yes, return true.  
Otherwise, return false.