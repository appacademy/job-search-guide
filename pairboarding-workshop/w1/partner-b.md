# Partner B

## Bridging the Gap

Tell me about a time when you linked two or more problems together and identified an underlying issue? Were you able to find a solution?

## Print Bridges
Write a function that takes in a graph and prints out the edges that are bridges.  A bridge is an edge whose deletion will cause the graph to become disconnected.  See diagram below.

![](bridge.png)

## Hints
A simple approach would be remove each edge from the graph one by one and run BFS/DFS starting from any vertex.  If the BFS/DFS covers all nodes than the removed edge cannot be a bridge.  Otherwise the edge is a bridge.  The time complexity of this solution is O(e(v + e)) where V is the the number of vertices and e is the number of edges in the graph.

## Solution
We can improve upon the above idea to get our solution down to O(n + m), where n is the number of vertices and m is the number of edges in the graph, by modifying our DFS to handle this problem in one pass.

We can say that the graph is 2 edge connected and therefore not a bridge if for every edge u -> v in the graph, there is at least one back-edge that is going out of the subtree rooted at v to some ancestor of u.  When we say subtree rooted at v, we mean all v's descendants include the vertex itself.

In other words, when we backtrack from a vertex v, we need to ensure that there is some back-edge from some descendant of v (including v) to some proper ancestor (parent or above) of v.

We can modify DFS such that DFS(v) returns the smallest arrival time to which there is a back edge from the sub-tree rooted at v.  For example, let arrival (v) be the arrival time of vertex v in the DFS.  Then if there is a way back from the sub-tree rooted at v, it's to something visited before v & therefore with a smaller arrival value.  Remember for a back edge ```u -> v``` in a graph, ```arrival[u] > arrival[v]```.

Suppose there are four edges going out of a sub-tree rooted at v to vertex a, b, c & d and with arrival time A(a), A(b), A(c), A(d) respectively.  We look at their four arrival times & consider the smallest among them and that will be the value returned by DFS(v). i.e. DFS(v) returns minimum of (A(a), A(b), A(c), A(d)). Before returning we have to check that min (A(a), A(b), A(c), A(d)) is less than A(v).  If min (A(a), A(c), A(d)) is less than A(v), then that means that at least one back-edge is going out of the sub tree rooted at v.  If not, we can say that (parent[v], v) is a bridge.

``` javascript
class Edge {
  constructor(source, dest) {
    this.source = source;
    this.dest = dest;
  }
}

class Graph {
  constructor(edges, n) {
    this.adjList = new Array(n);
    for (let i = 0; i < n; i++) {
      this.adjList[i] = [];
    }

    // add edges to the undirected graph
    for (let i = 0; i < edges.length; i++) {
      let src = edges[i].source;
      let dest = edges[i].dest;
      this.adjList[src].push(dest);
      this.adjList[dest].push(src);
    }
  }
}

const printBridges = (graph, v, discovered, arrival, parent, time) => {
  // Perform DFS on graph starting from vertex v and find
  // all Bridges in the process

  // set arrival time of vertex v
  time += 1
  arrival[v] = time

  // mark node as discovered
  discovered[v] = true;

  // initialize arr to be the arrival time of vertex v
  let arr = arrival[v];


  // (v, i) forms an edge
  let adjList = graph.adjList[v];
  for (let i = 0; i < adjList.length; i++) {

    // if i is not discovered
    if (discovered[adjList[i]] === undefined) {
      arr = Math.min(arr, printBridges(graph, adjList[i], discovered, arrival, v, time))

      // i is discovered but is not a parent of v
    } else if (adjList[i] !== parent) {

      // if the vertex i is already discovered, that
      // means that there is a back edge starting from
      // v.  Note that discovered[i] is already true,
      // arrival[i] is already defined.
      arr = Math.min(arr, arrival[adjList[i]]);
    }
  }

  // if value of arr remains unchanged ie. it's equal
  // to the arrival time of vertex v and if v is not root
  // node, then (parent[v] -> v) forms a Bridge
  if (arr === arrival[v] && parent !== -1){
    console.log("Bridge: " + parent + ", " + v)
  }

  // we return the minimum arrival time
  return arr
}

let edges = [
  new Edge(0, 2),
  new Edge(1, 2),
  new Edge(2, 3),
  new Edge(2, 4),
  new Edge(3, 4),
  new Edge(3, 5)
  ];

let n = 6;

let discovered = new Array(n);
let arrival = new Array(n)
for(let i = 0; i < n; i++) {
  arrival[i] = i;
}
let start = 0;
let parent = -1;
let time = 0;

let graph = new Graph(edges, n)

printBridges(graph, start, discovered, arrival, parent, time)
```
