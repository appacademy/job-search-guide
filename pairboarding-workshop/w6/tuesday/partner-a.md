# Partner A

## Time to innovate
* Give me an example of a time you used customer feedback to drive improvement or innovation.
* What was the situation and what action did you take?

## Floating Point Precision

* What will the code below output? Explain your answer.

```JavaScript
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```

### Answer
An educated answer to this question would simply be: “You can’t be sure. it might print out `0.3` and `true`, or it might not. Numbers in JavaScript are all treated with floating point precision, and as such, may not always yield the expected results.”

The example provided above is classic case that demonstrates this issue. Surprisingly, it will print out:

```JavaScript
0.30000000000000004
false
```

A typical solution is to compare the absolute difference between two numbers with the special constant `Number.EPSILON`:

```JavaScript
function areTheNumbersAlmostEqual(num1, num2) {
	return Math.abs( num1 - num2 ) < Number.EPSILON;
}
console.log(areTheNumbersAlmostEqual(0.1 + 0.2, 0.3));
```

## River Sizes
You are given a two-dimensional array (matrix) of potentially unequal height and width containing only 0s and 1s.  Each 0 represents land, and each 1 represents part of a river.  A river consists of any number of 1s that are either horizontally or vertically adjacent (but not diagonally adjacent).  The number of adjacent 1s forming a river determines its size.  Write a function that returns an array of the sizes of all rivers represented in the input matrix.  **Note that these sizes do not need to be in any particular order.**

Sample Input:
```JavaScript
[
  [1,0,0,1,0],
  [1,0,1,0,0],
  [0,0,1,0,1],
  [1,0,1,0,1],
  [1,0,1,1,0]
]
```
Sample Output:
```JavaScript
=> [1,2,2,2,5]
```

### Answer
This is a classic graph traversal problem.  To solve it, we'll iterate through the array/graph, treating each value as a node. If the node hasn't been seen and it's value is a `1` we'll preform a depth first search on it.  We'll consider each neighboring node ignoring nodes that are `0`s or `1`s that we've already seen.  When we do encounter a new `1` we'll increment our `currentRiverSize` and perform DFS again, this time with this new `1` as the root node.  When there are no more nodes left to explore, we'll push the currentRiverSize into our result array and continue iterating through our graph.  At the end we return our result array.  This function will run in **O(n) time and O(n) space** where n is the total number of elements in the input matrix.  The analysis on this problem can be a little tricky so let's break it down.  We're iterating through every input in the array so that's O(n) but what about all the other operations we're doing?  Well it turns out that our DFS is only exploring unexplored nodes, if it does encounter a previously seen node it's skipping it, a constant time operation.  Not only that, but we're marking nodes as visited during our DFS allowing us to skip them later when we encounter them a 2nd time in our iteration, therefore our time complexity remains at O(n).

```JavaScript
// helper function to get unvisited neighboring nodes
const getUnvistitedNeighbors = (i, j, matrix, visited) => {
  const unvisitedNeighbors = [];
  if (i > 0 && !visited[i - 1][j]) unvisitedNeighbors.push([i - 1, j]);
  if (i < matrix.length - 1 && !visited[i + 1][j]) unvisitedNeighbors.push([i + 1, j]);
  if (j > 0 && !visited[i][j - 1]) unvisitedNeighbors.push([i, j - 1]);
  if (j < matrix[0].length - 1 && !visited[i][j + 1]) unvisitedNeighbors.push([i, j + 1]);
  return unvisitedNeighbors;
}

// helper function to traverse nodes (essentially DFS)
const traverseNode = (i, j, matrix, visited, sizes) {
  let currentRiverSize = 0;

  // stack to hold nodes we're still exploring
  const nodesToExplore = [[i, j]];

  // DFS
  while (nodesToExplore.length > 0) {
    const currentNode = nodesToExplore.pop();
    [i, j] = [currentNode[0], currentNode[1]];    
    // continue if we've already seen the node or it's a zero
    if (visited[i][j]) continue;
    visited[i][j] = true;
    if (matrix[i][j] === 0) continue
    // node was neither a zero nor visited so we increment river size
    currentRiverSize++;
    const unvisitedNeighbors = getUnvistitedNeighbors(i, j, matrix, visited);    
    for (let i = 0; i < unvisitedNeighbors.length; i++) {
      nodesToExplore.push(neighbor);
    }
  }
  if (currentRiverSize > 0) sizes.push(currentRiverSize);
}

const riverSizes = (matrix) => {
  // array to hold our result
  const sizes = [];  
  // a 2d array to keep track of visited nodes
  const visited = matrix.map(row => row.map(value => false));
  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix.length; j++) {      
      // if node is on the visited list - skip it
      if (visited[i][j]) continue;
      traverseNode(i, j, matrix, visited, sizes);
    }
  }
  return sizes;
}
```
