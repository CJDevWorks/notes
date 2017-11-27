Graphs
===============

- Types :
Directed 
Undirected

- Representation


- Weighted graphs Vs UnWeighted graph
    Representation

- Common operation :

Finding cycle in graph

Common Traversal algorithm
==================================

Depth first
=======================

Breadth first
========================
Shortest path for unweighted graph (identifies least no of intermediate node)


Dijkstra’s algorithm
===============================

- Dijkstra’s algorithm only works with directed acyclic graphs, called DAGs for short.
- You can’t use Dijkstra’s algorithm if you have negative-weight edges (Once you process a node,         it means 
there’s no cheaper way to get to that node) 

1.  Find the cheapest node. This is the node you can get to in the least amount of time.

2.  Check whether there’s a cheaper path to the neighbors of this node. If so, update their costs. 
                                               
3.  Repeat until you’ve done this for every node in the graph. 
 
4.  Calculate the final path. (Coming up in the next section!)
