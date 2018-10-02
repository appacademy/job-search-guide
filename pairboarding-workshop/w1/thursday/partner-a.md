# Partner A

NB: Today's pairboarding session focuses on refreshing the skills you learned during the job search. If you feel as if you have mastered topological sort, try solving some medium/hard [LeetCode](https://leetcode.com/problemset/all/?topicSlugs=graph) problems related to graphs.

## Playing Nice

Do you do your best work alone or in a group?  Does the type of work matter?

## Kahn's Algorithm

Implement topological sort using Kahn's algorithm. Assume the following setup:

```ruby
class Vertex
  attr_reader :value, :in_edges, :out_edges

  def initialize(value)
    @value, @in_edges, @out_edges = value, [], []
  end
end

class Edge
  attr_reader :to_vertex, :from_vertex, :cost

  def initialize(from_vertex, to_vertex, cost = 1)
    self.from_vertex = from_vertex
    self.to_vertex = to_vertex
    self.cost = cost

    to_vertex.in_edges << self
    from_vertex.out_edges << self
  end

  def destroy!
    self.to_vertex.in_edges.delete(self)
    self.to_vertex = nil
    self.from_vertex.out_edges.delete(self)
    self.from_vertex = nil
  end

  protected
  attr_writer :from_vertex, :to_vertex, :cost
end
```

If your partner needs a hint, you can walk them through the following steps:

* Determine the in-edge count of each node.
* Collect nodes with zero in-edge count in a queue.
* While the queue is not empty:
  - Pop node `u` from queue,
  - remove `u` from the graph (depending on your implementation, this may or may not involve the `destroy!` method; what are the complications to destroying as we loop? What is another way we can track the number of `in_edges`?),
  - check if there is a new node with in-degree zero (among the neighbors of `u`)
  - If yes, put that node into the queue.
  - We maintain a list that records in which order the nodes are removed.
* If the queue is empty:
  - if we removed all nodes from the graph, return the list
  - else we return an empty list that indicates that an order is not possible due to a cycle
  
### Solution

```ruby
def topological_sort(vertices)
  in_edge_counts = {}
  queue = []

  vertices.each do |v|
    in_edge_counts[v] = v.in_edges.count
    queue << v if v.in_edges.empty?
  end

  sorted_vertices = []

  until queue.empty?
    vertex = queue.shift
    sorted_vertices << vertex

    vertex.out_edges.each do |e|
      to_vertex = e.to_vertex

      in_edge_counts[to_vertex] -= 1
      queue << to_vertex if in_edge_counts[to_vertex] == 0
    end
  end

  sorted_vertices
end
```

## First Contact

Given a sorted dictionary (array of words) of an alien language, find the order of the characters in the language.

### Example
```
Input:  words = ["baa", "abcd", "abca", "cab", "cad"]
Output: 'b', 'd', 'a', 'c'
```
Note that words are sorted and in the given language "baa" comes before "abcd", therefore 'b' is before 'a' in output. Similarly, we can find other orders:
```
Input:  words = ["caa", "aaa", "aab"]
Output: 'c', 'a', 'b'
```

### Solution

We can solve this problem by creating vertices of the characters, then finding the topological sorting of the vertices.

* Create a number of vertices equal to the size of alphabet in the given alien language. For example, if the alphabet size is 5, then there can be 5 characters in words. 

* For every pair of adjacent words in given sorted array:
  * Let the current pair of words be word1 and word2. One by one compare characters of both words and find the first mismatching characters.
  * Create an edge from the mismatching character of word1 to that of word2.
* Print the topological sorting of the vertices.

```ruby
def alien_letter_order(words)
  vertices = {}
  
  words.reduce(:+).split('').uniq.each do |letter|
    vertices[letter] = Vertex.new(letter)
  end
  
  (0...words.length).each do |i|
    word1, word2 = words[i], words[i + 1]
    smaller = word1.length < word2.length ? word1.length : word2.length
    
    (0...smaller).each do |j|
      if word1[j] != word2[j]
        Edge.new(vertices[word1[j]], vertices[word2[j]])
        break
      end
    end
  end
  
  topological_sort(vertices.values).map { |v| v.value }
end
```

### Discuss:
* What are the time and space complexities of this method?

### Credit:
* Adapted from [this](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/) Geeks for Geeks problem.
