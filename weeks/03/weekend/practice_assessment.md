# 🚨 Practice Test 🚨 

Welcome to the end of Week 3! The next step is to double down on what you've learned, and prepare for the HackerRank test that will be will be in the following task. The first step is to work through this practice test to have an idea of what to expect on the HackerRank exam.

Before you dive into the HackerRank test, it's important to review. We use the HackerRank test results to gauge your progress in the job search guide, so you'll want to make sure you are as prepared as possible. If you struggle on this practice exam, be sure to review flash cards!

Make an honest effort with these problems. An answer key is at the bottom of the page, but try and review your notes and readings before referring to these. 

1.) Choose the correct statement(s) about heaps
  * A) A heap can be represented as a type of tree structure
  * B) Heaps can be used to find the average element in better time than you can by using an unstructured array
  * C) A heap can be used to find the largest `n/2` elements in O(n/2*logn) time
  * D) Heapifying down will work no matter which child you choose to swap with a parent
  * E) As soon as a parent element fulfills the heap property with one of its children, the heapify down operation can end
  * F) Heapifying always takes log(n) time
  * G) Heapifying up is less costly than heapifying down
  * H) Heaps can only be made into priority queues if we compare number values for each element
  * I) In a heap you can have any number of children for each parent element and it will still behave like a heap
2.) Which statement(s) about the page lifecycle is/are correct?
  * A) Once DOMContentLoaded fires, you have access to any resource you need on the page, including images
  * B) A `<script>` tag in the middle of your HTML won't prevent the rest of the DOM from being loaded.
  * C) `<script>`s that load from an external source don't interrupt the page loading while they are being downloaded, but do interrupt it while they are executing
  * D) `async` and `defer` can only be used on external scripts
  * E) `async` and `defer` scripts execute whenever they are ready
  * F) `defer` scripts execute in document order
  * G) `defer` scripts can be relied on to have access to any DOM element they need, even though they are executed before DOMContentLoaded
3.) Select the correct statement(s) about React/Redux
  * A) Container components do not have their own props
  * B) the `connect` function is required to create a container component because there is no other way to access state
  * C) the `connect` function is how a container component gains access to the 'dispatch' function defined on the store
  * D) `connect` takes two arguments and returns a function that must be invoked
  * E) mapStateToProps and mapDispatchToProps are both expected to return objects
4.) Choose the correct statement(s) about AJAX and XHR
  * A) XHR objects are built into JavaScript
  * B) XHR objects have a property `onreadystatechange` that can be assigned a callback function that will only be invoked when the request is completed successfully
  * C) XMLHttpRequest.open() accepts a parameter that can be used to execute the .send() method synchronously
  * D) The url is provided in the .send method
  * E) The only way to write a truly asynchronous AJAX request is by using the jQuery library
5.) Which statement(s) about heaps and heapsort is/are correct?
  * A) Building a heap by iterative insertion has linear time complexity for a sufficiently randomized dataset
  * B) There is no way to guarantee linear time for building a heap
  * C) heapsort in-place can be done recursively
  * D) heapsort in-place is a stable sorting algorithm because we don't use any extra memory
  * E) heapsort in-place involves extracting elements into another data structure and is complete when the original input has no more elements remaining
  * D) Every set of data has a unique heap that can represent it
6.) Choose the correct statement(s) about variables in JavaScript
  * A) variables defined without keywords will always throw an error
  * B) `let` and `const` are hoisted to the nearest function scope
  * C) `var`s that are declared outside of any function scope will have their assignments hoisted to the top of the code
  * D) variables defined in a `for` loop cannot be accessed from functions defined outside that `for` loop
  * E) This code will not throw an error:
  ```javascript
    function func() {
      for (let i = 0; i < 5; i++) {
        func2()
      }
      function func2() {
        console.log(i);
      }
    }
    func()
  ```
  * F) This code will not throw an error:
  ```javascript
    function func() {
      for (var i = 0; i < 5; i++) {
        func2()
      }
    }
    function func2() {
      console.log(i);
    }
    func()
  ```
  * G) `const` variables cannot be redefined, but the contents of the objects assigned to them can be mutated
7.) Choose the correct statement(s) about CORS and same-origin policy
  * A) `img`s are typically allowed to be accessed cross-origin
  * B) you can allow a resource to be loaded cross-origin by setting the `Access-Control-Allow-Origin` header on your request
  * C) CORS preflight can tell you whether your request method will be accepted by the server
  * D) same-origin policy means that two requests to two different pages on the same domain have to both come from your computer
  * E) Requests for resources made from a backend server are not subject to CORS restrictions because unlike a browser, the HTTP clients used do not implement the same-origin policy.
  * F) same-origin policy can help prevent DDoS attacks
8.) Choose the correct statement(s) about MergeSort
  * A) MergeSort is unstable because elements that are of the same value might end up in different positions relative to one another
  * B) MergeSort takes up log(n) extra space because of the depth of the stack you create
  * C) the merge() function requires that the arrays being merged are of the same size
  * D) the merge function requires that the inputs each be internally sorted already in order to work
  * E) the time complexity for MergeSort is always nlogn
9.) Select the correct statement(s) about strict mode and the `rest` and `spread` operators
  * A) strict mode prevents you from hoisting `var`s to the global scope
  * B) strict mode prevents you from duplicating variable names
  * C) strict mode prevents you from naming variables certain protected keywords
  * D) strict mode requires you to use the `rest` operator because the `arguments` keyword is protected
  * E) `rest` can be used to automatically create a `for` loop over the remaining items in an arrays
  * F) the `spread` operator can be used to replicate the data of one array without copying the reference to that array
  * G) `function(...Dogs)` defines an immutable Dogs object
10.) Which statement(s) about SQL is/are correct?
  * A) The SELECT keyword is evaluated first, meaning that only those columns are considered in the WHERE clause
  * B) WHERE acts as a prefilter, while HAVING acts as a postfilter
  * C) HAVING can be seen as a WHERE clause in a subquery
  * D) aggregate functions are unavailable in a WHERE clause
  * E) Nested queries cannot use the HAVING clause

