# Partner B

## Home Improvement

Tell me about a time you improved a tool, task, or project you were working on. What was the circumstances? Why did you do it?  Do you have any other examples?

## Tarjan's Algorithm

Implement topological sort using Tarjan's Algorithm.

If your partner needs a hint, walk them through this description:

The algorithm loops through each node of the graph, in an arbitrary order, initiating a depth-first search that terminates when it hits any node that has already been visited since the beginning of the topological sort or the node has no outgoing edges (i.e. a leaf node):

Each node n gets prepended to the output list L only after considering all other nodes which depend on n (all descendants of n in the graph). Specifically, when the algorithm adds node n, we are guaranteed that all nodes which depend on n are already in the output list L: they were added to L either by the recursive call to visit() which ended before the call to visit n, or by a call to visit() which started even before the call to visit n.

Cycle catching can be tricky - try without it first.

### Solution

```ruby
def topological_sort(vertices)
  order = []
  explored = Set.new
  temp = Set.new
  cycle = false

  vertices.each do |vertex|
    cycle = dfs!(vertex, explored, temp, order, cycle)  unless explored.include?(vertex)
    return [] if cycle
  end

  order
end


def dfs!(vertex, explored, temp, order, cycle)
  return true if temp.include?(vertex)
  temp.add(vertex)

  vertex.out_edges.each do |edge|
    next_vertex = edge.to_vertex
    cycle = dfs!(next_vertex, explored, temp, order, cycle) unless explored.include?(next_vertex)
    return true if cycle
  end

  explored.add(vertex)
  temp.delete(vertex)
  order.unshift(vertex)
  false
end
```

## [Bonus Problem](https://www.geeksforgeeks.org/snake-ladder-problem-2/)
