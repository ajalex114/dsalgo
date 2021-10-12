---
layout: post
title: Tree - Level Order Traversal
categories: [Tree, Medium]
---

Language: `C#`

## Problem Statement

Level Order Traversal

```
Input: 
       1       
    2     3
 4     5

Output: 1 2 3 4 5
```

## Solution

### Tree Data Structure

``` csharp
class Node
{
    public int Data;
    public Node Left;
    public Node Right;

    public Node(int data)
    {
        Data = data;
    }

    public Node(int data, Node left, Node right)
    {
        Data = data;
        Left = left;
        Right = right;
    }
}
```

### Populate Tree

``` csharp
var root = new Node(1, new Node(2, new Node(4), new Node(5)), new Node(3));
```

### Level Order Traversal

``` csharp
void LOT()
{
    Queue<Node> q = new();
    q.Enqueue(root);

    while (q.Count > 0)
    {
        var node = q.Dequeue();

        if(node is not null)
        {
            if (node.Left is not null)
                q.Enqueue(node.Left);

            if (node.Right is not null)
                q.Enqueue(node.Right);

            Console.WriteLine(node.Data);
        }
    }
}
```

## Complexity

Time Complexity: `O(N)`  
Space Complexity: `O(N)`  
