---
layout: post
title: LC 735 Asteroid Collision
categories: [LeetCode, Array, LinkedList, Medium, G, M, U, F, A]
---

LeetCode Link: [https://leetcode.com/problems/asteroid-collision/](https://leetcode.com/problems/asteroid-collision/)  
Language: `C#`

# Problem Statement #

We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

## Examples

Example 1:

```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.
```

Example 2:

```
Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
```

Example 3:

```
Input: asteroids = [10,2,-5]
Output: [10]
Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.
```

Example 4:

```
Input: asteroids = [-2,-1,1,2]
Output: [-2,-1,1,2]
Explanation: The -2 and -1 are moving left, while the 1 and 2 are moving right. Asteroids moving the same direction never meet, so no asteroids will meet each other.
```

## Constraints  

* 2 <= asteroids.length <= 104
* -1000 <= asteroids[i] <= 1000
* asteroids[i] != 0

# Solution

``` csharp
public class Solution 
{
    public int[] AsteroidCollision(int[] asteroids) 
    {
        var len = asteroids.Length;
        if (len < 2)
        {
            return asteroids;
        }
        
        var list = new LinkedList<int>(asteroids);
        var node = list.First;
        
        while (node != null)
        {
            var next = node.Next;
            if (next != null)
            {
                if (IsPositive(node.Value) && !IsPositive(node.Next.Value) &&
                   Math.Abs(node.Value) > Math.Abs(node.Next.Value))
                {
                    next = node;
                    var temp = node.Next;
                    list.Remove(temp);
                }
                
                else if (IsPositive(node.Value) && !IsPositive(node.Next.Value) &&
                   Math.Abs(node.Value) < Math.Abs(node.Next.Value))
                {
                    next = node.Next;
                    if (node.Previous != null)
                    {
                        next = node.Previous;
                    }
                    list.Remove(node);
                }
                
                else if (IsPositive(node.Value) && !IsPositive(node.Next.Value) &&
                   Math.Abs(node.Value) == Math.Abs(node.Next.Value))
                {
                    var temp = node.Next;
                    next = node.Next.Next;
                    
                    if (node.Previous != null)
                    {
                        next = node.Previous;
                    }

                    list.Remove(node);
                    list.Remove(temp);
                }
                else 
                {
                    next = node.Next;
                }                
            }
            node = next;
        }
        
        return list.ToArray();
    }
    
    private bool IsPositive(int num) => num >= 0;
}
```

# Notes

Please note to move back or stay on the same node, if you remove a particular node.  
This is so that, you compare the current node with the next available node as well after removing a node.

For instance:

Consider the example:

`[1,3,-2,-3,-1]`  

In this case, 

Once you reach node 3, you see that -2 is smaller, hence you delete -2.  
Now stay on 3 itself.  
`[1,3,-3,-1]`  

Now compare 3 and -3.  
Both of them are removed.  
Now step back, not forward.

`[1, -1]`

This now removes all of it.

## Complexities

**Time Complexity**: `O(N)`  
**Space Complexity**: `O(N)`
