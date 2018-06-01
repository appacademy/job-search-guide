# Graphs

### How do we define a graph, and where are they commonly used?
* In a tree with N nodes, we always have exactly N - 1 edges. Every node except the root node has exactly 1 parent. 1 possible path from root to any particular node
* a Graph G is an ordered pair of a set V of vertices and a set E of edges 
  * Set of vertices: `{ V1, V2, V3, V4, V5, V6, V7 }`
  * Set of edges: `{ {V1, V2}, {V2, V3}, {V4, V2} }`
* Edges can be both directed and undirected
  * For directed edges, there is an `origin` and `destination`. If we have a path from `V1` to `V2`, this does NOT mean we have a path from `V2` to `V1`
* Thus, Graphs can be directed and undirected.
* Example: Social Network (Undirected)
  * a Social Network is undirected graph
  * How would you model a friend suggestion algorithm?
* Example: Pages as Nodes (Directed)
  * If page B has a link to page A, page A doesn't necessarily have a link back to page B
* Graphs can be both Weighted and Unweighted 
  * An intercity network - Weighted Undirected (you can get back from any city you wish)
  * An intracity network - Weight directed graph (there will be some one-ways inside of a city)

### What are the specific attributes that graphs can have, and how do we talk about them?
* Self loop: When a node can have an edge that goes to itself 
* Multi-edge: Multiple edges from one vertex to another, often with different weights
  * There may be multiple flights from one city to another with different costs
* If a graph contains no self-loop or multi-edge, it is called a "Simple Graph" 
* What is the maximum number of edges in a simple graph?
  * In a directed graph, `N * (N - 1)`
  * In an undirected graph, `N * (N - 1) / 2`
* A Graph is called `Dense` if number of edges is close to maximum (on the order of square of vertices)
  * We store a dense graph in an adgency matrix
* A graph is called `Sparse` if a number of edges is closer to the number of Vertices.
  * We store a sparse graph in an adgency list 
* `Path` is a sequence of vertices where each adjacent pair is connected by an edge 
* `Simple Path` a path in which no vertices (and thus no edges) are repeated. 
> In graph theory, there is inconsistency with the word "path". Many say a Walk is any sequence of vertices. A path is when no vertices are repeated. A trail is a walk where no edges are repeated 
* A graph is called `strongly connected` if there is a path from any vertex to any other vertex (Directed Graph)
* A graph is called `connected` if it is undirected 
* If a directed graph is not strongly connected, but can be turned into an undirected graph, it is considered `weakly connected`
* A Walk is called a closed walk if it starts and ends at the same vertex 
* A `Simple Cycle` is a closed walk where there is no repetition other than start and end. 
* A graph with no cycle is called an `Acyclic Graph`

### What are some ways we might store a graph in memory? What space/time complexity problems might we face? 

* To create a store a graph in computers memory, we can create two dynamic lists (vector - C++, ArrayList - Java)
  * Vertex List
  * Edge List
* An edge is identified by its two endpoints. An edge is an object with two fields, so we can create an object 
  ```c
  struct Edge 
  {
    char *startVertex;
    char *endVertex;
  };
  ```
#### Space Complexity
* The space complexity of storing the Vertex List would be `O(|v|)`
* When storing edges, you must keep a reference to the vertex. One way to do this would be to keep reference to the position (index) of those edges. Space complexity would be `O(|e|)`
* Total Space: `O(|v| + |e|)`
#### Time Complexity
* How much time will you take to find all nodes adgacent to a given node? 
  * Running time for this operation would be `O(|e|)`
* Check if given nodes are connected 
  * Also `O(|e|)`
  * Remember that the number of edges is on the order of `v^2`

The takeaway is that this way of storing a graph is **not** very efficient!

