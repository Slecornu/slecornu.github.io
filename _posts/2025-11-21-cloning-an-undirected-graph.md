---
title: "Cloning an undirected graph"
date: 2025-11-21T22:25:00+00:00
categories:
  - DSA
---

## LeetCode Exercise: [133 Clone Graph](https://leetcode.com/problems/clone-graph/)

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

``` Kotlin
class Node(var `val`: Int) {
    var neighbors: ArrayList<Node?> = ArrayList<Node?>()
}
```

## My solution

To solve this, I used Depth-First Search to navigate the node structure. When I encountered a new node I stored them in a map, using their value as a key to prevent reacreating the node and to access their references in constant time.

``` Kotlin
class Solution {

    val map = HashMap<Int, Node>()

    fun cloneGraph(node: Node?): Node? {
        val value: Int = node?.`val` ?: return null
        
        if (map.containsKey(value)) {
            return map.get(value)
        }

        val clonedNode = map.getOrPut(value) { Node(value) }
        
        for (neighbour in node.neighbors) {
            cloneGraph(neighbour)?.let{
                clonedNode.neighbors.add(it)
            }
        }


        return clonedNode
    }
}
```

The time complexity of your algorithm is *O(V + E)*, where:
- *V* = number of vertices (nodes)
- *E* = number of edges

The space complexity is *O(V*), where the HashMap stores all *V* nodes.
