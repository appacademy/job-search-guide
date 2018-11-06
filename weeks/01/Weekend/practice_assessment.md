# 🚨 Practice Test 🚨 

Welcome to the end of Week 1! The next step is to double down on what you've learned, and prepare for the HackerRank test that will be in the following task. The first step is to work through this practice test to have an idea of what to expect on the HackerRank exam.

Before you dive into the HackerRank test, it's important to review. We use the HackerRank test results to gauge your progress in the job search guide, so you'll want to make sure you are as prepared as possible. If you struggle on this practice exam, be sure to review flash cards!

Make an honest effort with these problems. An answer key is at the bottom of the page, but try and review your notes and readings before referring to these. 

### Questions:

1. Which is/are the correct statement(s) about Adjacency Matrices and/or Adjacency Lists as ways to model a Graph?
  * A) An Adjacency Matrix takes O(n^2) space and provides O(V) for finding all adjacent nodes to a certain node (correct)
  * B) An Adjacency List takes O(V) space and O(E) time to find all nodes adjacent to another node
  * C) Adjacency Matrix and Adjacency List have equivalent space requirements, but a Matrix gives O(1) lookup for finding if two nodes are connected.
  * D) Both will give all the nodes connected to a certain node in O(E) time

2. Which of these is/are correct statement(s) about prototypes in JavaScript?
  * A) A prototype's constructor property must refer back the the same constructor function that has the prototype set as its `function.prototype`
  * B) functions will automatically create prototype objects that have the function itself set as `object.constructor`
  * C) `object.__proto__` always gives a reference to `object.constructor.prototype` even if that has been reassigned
  * D) objects cannot redefine properties that are defined on `object.__proto__`
  * E) the `new` keyword can be applied to all functions that aren't arrow functions, even if the function does not return an object.

3. Which of the following are true?
  * A) HTML allows for greater accessibility through semantic tags
  * B) Media queries allow you to detect tablet orientation
  * C) Media queries should not be used with CSS Grid
  * D) HTML5 introduced Flexbox, Canvas, and iFrames
  * E) HTML5 provides a History API that Javascript can interact with
  * F) Media queries are less important when implementing 'Mobile-first' development
  * G) CSS Grid lets you define and name areas of your page, but these named areas are not accessible through JS methods.
  * H) CSS Grid eliminates the need to use eventHandlers to dynamically change classes on DOM elements in order to create responsive layout

4. A RESTful API should allow for resources to be accessed and manipulated through: (choose any that apply)
  * A) instructions on what to do to the object in question
  * B) sending HTTP requests to stable URIs that specify the id of the object in the URI
  * C) DELETE requests that include the id of the resource in the body of the request
  * D) sending complete representations of the resource

5. Which of the following represent(s) a closure?

  * A) 
  ```javascript
  const feet = 'hands';
  let monkey = () => {
    console.log(`my feet are ${feet}`);
  }
  monkey();
  ```

  * B)
  ```javascript
  let dolphin = () => {
    const feet = 'flippers';
    console.log(`my feet are ${feet}`);
  }
  dolphin();
  ```

  * C)
  ```javascript
  function animal(name, hands) {
    console.log(`${name} has ${hands} for hands`);
  }
  var name = 'chicken';
  var hands = 'wings';
  animal(name, hands);
  ```

  * D)
  ```javascript
  function animal(myName, hands) {
    console.log(`${name} has ${hands} for hands`);
  }
  var name = 'duck';
  var hands = 'wings';
  animal("chicken", hands);
  ```

6. Pick the correct statement(s) about BFS and DFS
  * A) DFS requires passing a stack as an argument to successive recursive calls
  * B) BFS can be implemented using a queue and adding children to the queue every time an element is evaluated
  * C) BFS cannot be written recursively
  * D) DFS begins evaluating elements once an element has no children
  * E) BFS begins processing elements once all children are stored in a data structure
  * F) DFS cannot work on a cyclic graph, but BFS can
  * G) DFS will generally find an element faster than BFS, but uses more space
  * H) BFS can work by evaluating elements when they come off the queue or when they enter the queue
  * I) BFS and DFS can be performed on an undirected graph where there is no concept of children

7. Which statement(s) about the event loop in JavaScript and its interactions are correct?
  * A) The event loop itself is not responsible for choosing when to rendering new frames
  * B) The event loop refers to the asynchronous behavior of browser API functions like setTimeout
  * C) Once an asynchronous function completes, its callback is placed on top of the runtime stack
  * D) The runtime stack immediately invokes setTimeout when it appears in the code
  * E) Asynchronous functions enter into the callback queue until they are complete
  * F) The event loop uses the multi-threaded capabilities of the JavaScript runtime to execute asynchronous callbacks

8. When you type 'google.com' into your browser and hit enter...(select all that apply)
  * A) Your local ISP figures out what that means and sends your request to the correct IP address immediately
  * B) Your computer might already know the address to send your request to
  * C) The correct path to google's servers is sent back to you by the DNS servers
  * D) Your router is told by your ISP the exact node that your router should forward your request to
  * E) Google knows where to send the response back once it receives the request

9. Choose the correct statement(s) about the mounting phase of the React lifecycle
  * A) componentDidMount is the preferred place to attach eventHandlers
  * B) componentWillMount is where AJAX calls should be initialized to ensure that data is ready by the time the DOM is rendered
  * C) componentWillReceiveProps will be called in the mounting phase, letting you decide whether to call other methods based on the value of the props
  * D) componentWillMount is often used for App configuration
  * E) You can't call this.setState in componentWillMount because the object's constructor hasn't been called yet
  * F) componentDidMount has access to child 'refs'

10. Which of the following statement(s) about Topological Sort is/are correct?
  * A) Kahn's algorithm requires that you know which nodes are root nodes
  * B) Data with cycles can be topologically sorted as long as there are root nodes with no dependencies
  * C) DFS Topological Sort can begin on a leaf node
  * D) Kahn's algorithm uses a queue and a hash as supplemental data structures
  * E) DFS Topological Sort prepends nodes with no unvisited children onto the output
  * F) Kahn's algorithm can always be completed without concern for which nodes we have seen before, but DFS Sort cannot
  * G) DFS Topological Sort must be done recursively

---
## No Peeking!

* [Answer Key]('https://github.com/appacademy/job-search-guide/tree/master/weeks/01/weekend/answer_key.md')
