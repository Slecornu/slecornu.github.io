---
title: "Graph Valid Tree"
date: 2025-11-22T10:07:00+00:00
categories:
  - DSA
---

## LeetCode Exercise: [261 Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)


You have a graph of n nodes labeled from 0 to n - 1. You are given an integer n and a list of edges where edges[i] = [ai, bi] indicates that there is an undirected edge between nodes ai and bi in the graph.

Return true if the edges of the given graph make up a valid tree, and false otherwise.

## My solution
``` Kotlin
class Solution {
    fun validTree(n: Int, edges: Array<IntArray>): Boolean {
        // convert edges to nodes
        val nodes: ArrayList<ArrayList<Int>> = ArrayList()
        for (n in 0 until n) {
            nodes.add(ArrayList())
        }

        for (edge in edges) {
            nodes.get(edge[0]).add(edge[1])
            nodes.get(edge[1]).add(edge[0])
        }

        // keep reference of parent nodes
        val parent:  HashMap<Int, Int> = HashMap()
        parent.put(0, -1)

        // keep reference of visited node
        val stack: Stack<Int> = Stack()
        stack.push(0)

        while (!stack.isEmpty()) {
            val node = stack.pop()
            for (neighbour in nodes.get(node)) {
                if (parent.get(node) == neighbour) {
                    continue
                }

                if (parent.containsKey(neighbour)) {
                    return false
                }

                stack.push(neighbour)
                parent.put(neighbour, node)
            }
        }

        return parent.size == n
    }
}
```
