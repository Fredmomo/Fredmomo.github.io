---
title: "Graph and Related Leetcode Problems"
description: "This post lists common algorithms about graph and some examples to practise."
pubDate: "Jan 12 2025"
heroImage: "/post_img.webp"
badge: "Demo badge"
tags: ["Leetcode","Graph"]
---

Graph is a kind of data structures that can be used to abstract different real-life data models, like all sorts of networks, routes, flows and connections.
Graph can be a directed graph which has directions betwwen each nodes or undirected graph which is a kind of bidirectional graph, both are desribed as graph G = (V, E) where V means Vertices and E means edges.
A binary tree and multi-children tree is a kind of special directed graph.

# 1. Graph traversal

Graph can be traversed using either depth-first search(DFS) or broadth-fist search(BFS), usually BFS is more efficient to get the shortest path in a graph (imagine you need to find the minimum hops from a start node to an end node, you start searching simultaneously, the node with minimum hops can always get returned immediately when found without continuing searching the rest). While DFS is better for do a thorough search in the whole graph. 

To traverse a tree, no matter what method you are using, you need a _visited_ hash set or boolean array to mark all the visited nodes to avoid duplicate visiting or a never-ending loop. 

For a BFS, you could use a queue ( _LinkedList_ in Java, _dequeue_ in Python, _std::queue_ in C++) to record the order for the traversing. While the queue is not empty, you iterate through all the current elements in the queue and pop/poll them out, finding all their neighbours and add to the queue for the next iteration, just need to be careful to get a fixed queue length for the iteration before adding more elements to it. Remember to check and return any desired item you find during the search.

Similarly for a DFS, you can either use a stack ( _Stack_ in Java, _dequeue_ or _list_ in Python, _std::stack_ in C++) to record the traversing order or using recurrsion.

The time complexity for a traverse is _O(V+E)_.

Examples of BFS and queue:

1. [Bus Route] (https://leetcode.com/problems/bus-routes/description/)
2. [Open the Lock](https://leetcode.com/problems/open-the-lock/description/)
3. [Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/description/)
4. [Word Ladder](https://leetcode.com/problems/word-ladder/description/)

Examples of DFS and stack:
1. [Number of Islands](https://leetcode.com/problems/number-of-islands/description/)
2. 

# 2. Adjacency Representation

We could use different kind of data structure to represent a graph, some typical ones are:

* Adjacency matrix

A 2-d array, the index of the array corresponds to the index of the node, the value represents either connection status (1 means connected, 0 otherwise) or edge weight in a weighted graph.

Two examples:
adj = [[0,1,0], [1, 0, 0], [0, 0, 1]]

adj = [[2,1,1],[2,3,1],[3,4,1]]

* Adjacency list

A linked list array, where each linked list represents the neighbours of the node whose index corresponds to the array list, for a weighted graph the element of the linked list could be a class Pair or simply an array with only two elements(i.e. the end node and the weight).

An example:
adj = new LinkedList<int[]>[] = [{[1,0.5],[2, 0.8]}, {[3, 0.7]}]

or adj = [{Pair(1, 0.5), Pair(2, 0.8)}, {Pair(3, 0.7),}]

# 3. Dijkstra Algorithm

It usually included a graph with different weight assigned to different edges (weighted graph), and you need to find a path or a minimum/maximum total value when traversing the graph from a start (to an end) node. 

Two examples of Leetcode problems:

1. [Network Delay TIme](https://leetcode.com/problems/network-delay-time/description/) : to find the minimum value
2. [Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/description/) : to find a maximum value 

Similar to dynamic programming you can resort to a list/array to keep record of the best result so far. To initialise the array, you could fill all the values to a max or min integer/float value.

In this kind of problems, you need to:

1. Use an array to record the best calculated values for each node from the starting point 
2. Add a new class that is used to save both the node number/index and the best calculated value from the starting point
3. Use a priority queue or a min/max heap to get the best nodes each time to boost performance (lifting time complexity from _O(V(V+E))_ to _O(logV(V+E))_.

# 4. Union Find

Union Find is to find the connectivity of the graph in a bunch of graphes, it's just like a forest containing with lots of trees, your job is mainly dealing with those trees to either connect them or identify them.

Two examples of Leetcode problems:

1. [Minimize Malware Spread](https://leetcode.com/problems/minimize-malware-spread/description/)
2. [Satisfiability of Equality Equations](https://leetcode.com/problems/satisfiability-of-equality-equations/description/)

You will need to class _UF_ or _Forest_ to keep record of all the vairiables including:

* An integer _count_ to keep record of the total number of trees in the forest
* An integer array _parent_ to keep record of the parent for each node in the forest
* An integer array _size_ to keep record of the total number of children that are connected to this node.

And it will need four functions:

* A constructor to build the forest and initialize each parent to be the node itself and the size to be 1, the _count_ should be the total number of nodes _n_
* A connection function _union_ to connect two trees together by first _find_ the roots of the given two root nodes and comparing the size of the two roots, connecting the smaller tree to a large tree to make it more balanced (Time complexity can be reduced from _O(n)_ to _O(logn)_ from a linked list to a complete balance tree)
* A root finding function _find_ to iterate throught the _parent_ array and return the index of the parent. To optimize, when iterating you can compress the root by setting the parent of the node's parent to become its direct parent to control the height of the tree. (To further reduce the time complexity from _O(logn)_ to _O(log3) = O(1)_)
* A function _isConnected_ to check if the two nodes are connected by finding their roots and compare if they are the same one.


