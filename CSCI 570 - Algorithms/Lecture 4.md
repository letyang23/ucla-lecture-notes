### Priority Queue

A priority queue has to perform these two operations fast!

1. Insert an element into the set
2. Find the smallest element in the set

Def. A binary tree of depth k which has exactly $2^k-1$ nodes is called a full binary tree.

Def. A binary tree with **n** nodes and of depth k is complete iff its nodes correspond to the nodes which are numbered **1 to n** in the full binary tree of depth k.

Traversing a complete binary tree stored as an array.

Def. A binary heap is a complete binary tree with the property that the value of the key at each node is at least as large as the key values at its children (maxheap)

Construction

Can be done in $O(n\log n)$ time using n insert operations.

Q: What is the best run time to merge two binary heaps of size n?

Finding the top k elements in an array.

Input: An unsorted array of length n

Output: Top k values in the array (k<n)

Constraints:

- You cannot use any additional memory	
- Your algorithm should run in time $O(n\log k)$





Problem Statement
Find a MST in an undirected graph
Sol 1:  Sort all edges in increasing order of cost. Add edges to T in this order as long as it does not create a cycle. If it does, discard the edge - Kruskal's Algorithm
Sol 2: Similar to Dijkstra's algorithm, start with a node set S (initially the root node) on which a minimum spanning tree has been constructed so far. At each step, grow S by one node, adding the node v that minimizes the attachment cost. - Prim's Algorithm
Sol 3: Backward version of Kruskal's. Start with a full graph. Begin deleting edges in order of decreasing cost as long as it does not disconnect the graph. - Reverse Delete Algorithm