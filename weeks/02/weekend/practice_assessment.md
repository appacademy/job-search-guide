# 🚨 Practice Test 🚨 

Welcome to the end of Week 2! The next step is to double down on what you've learned, and prepare for the HackerRank test that will be will be in the following task. The first step is to work through this practice test to have an idea of what to expect on the HackerRank exam.

Before you dive into the HackerRank test, it's important to review. We use the HackerRank test results to gauge your progress in the job search guide, so you'll want to make sure you are as prepared as possible. If you struggle on this practice exam, be sure to review flash cards!

Make an honest effort with these problems. An answer key is at the bottom of the page, but try and review your notes and readings before referring to these. 

### Questions:

1.) Select the correct statement(s) about recursion
  * A) Tail recursion eliminates the extra memory created in each stack by passing all the variables by reference to the next recursive call
  * B) The space cost for recursive binary search is O(n) if you don't create a new copy of the sliced array
  * C) Tail recursion requires that you don't use any variables in the last line of the code unless you are passing them as arguments to the recursive call
  * D) The space cost for MergeSort is log(n) because the depth of you stack is log(n)
2.) What is the correct output of this code:
  ```javascript
    console.log(b);
    console.log(a);

    try {
      func1(b)
    } catch(e) {
      console.log(e.name);
    }

    try {
      func2()
    } catch(e) {
      console.log(e.name);
    }

    var a = () => {
      console.log(this);
      var f = 'f'
      return {}
    }

    var b = {}

    function func1(c) {
      try {
        c.name = "win"
      } catch(e) {
        c = 'c'
        console.log(e.name);
      }
      console.log(c);
    }

    let d = 'd'

    func1(b)

    b = {'you': null}

    function func2() {
      a()
      console.log(f);
    }
  ```

  * A)
  ```javascript
    undefined
    undefined
    TypeError
    c
    {}
    ReferenceError
    { name: 'win' }
  ```

  * B)
  ```javascript
    undefined
    undefined
    TypeError
    c
    TypeError
    { name: 'win' }
  ```
 
  * C)
  ```javascript
    undefined
    undefined
    TypeError
    c
    TypeError
    { you: null, name: 'win' }

  ```

  * D)
  ```javascript
    undefined
    TypeError
    c
    TypeError
    [Function]
    { you: null, name: 'win' }
  ```

  * E)
  ```javascript
    {}
    [Function]
    TypeError
    c
    TypeError
    { name: 'win' }
  ```
3.) Select the correct statement(s) about Redux
  * A) Redux uses the idea of a single source of truth, the state tree, and it is a mutable object that can be mutated by many different functions
  * B) Reducers can call other reducers**
  * C) Unknown action types should return a new state object
  * D) if no state object is passed to a reducer, then it should return an empty object, because the intent was to clear state
  * E) functions that are subscribed to the store will fire when the store is changed
  * F) splice and concat are best to use in a reducer because they return new objects
  * G) Object.assign overwrites properties in order of how its arguments are received, even when the first object has those properties
  * H) combineReducers is shorthand syntax that defines the slices of state and which reducers to pass these slices to
  * I) React components will automatically render any children defined between their `<> </>` tags
  * J) Presentational components are more modular when they contain explicit declarations of all the functions they will attach to elements
  * K) The purpose of a container component is to subscribe to the store and to calculate the props that will be passed to the presentational component
4.) Select the correct statement(s) about HTTP methods and status codes
  * A) There is no HTTP method that will allow you to determine the accepted Content-Type Headers, so instead you must rely on status codes in the response
  * B) A 400-level code will be returned when there is an error in the backend code
  * C) A 404 error is what you could expect if you send a bad password to login
  * D) A 201 code could be what you should expect when you create a valid blog post
  * E) A 301 code could indicate that the data cached in your browser already matches what would be returned by your request
5.) Which statement(s) about recursion and iteration is/are correct?
  * A) Recursion is more suited to functional programming because you can more easily create stateless methods
  * B) By implementing a queue you can replicate recursive behavior within a single stackframe
  * C) Recursion always takes more space than iteration
  * D) Any recursive problem can be done iteratively
6.) Select the correct statement(s) about the `new` keyword
  * A) The `new` keyword can be applied to any function
  * B) It returns a new object, even if the function doesn't create one
  * C) It creates a new prototype that will be used in future calls to the same function
  * D) It sets a prototype on the object it returns
  * E) It sets the context of `this` within the function to the new object that the function will return
7.) Choose the correct statement(s) about Dynamic Programming
  * A) Tabulation will create a complete record of subsolutions from the Bottom-up
  * B) Memoization refers to a Top-down approach where you are guaranteed a complete set of subsolutions by the end
  * C) Overlapping subproblems is not a requirement for Dynamic Programming to be applicable
  * D) Optimal Substructure means that every time you store something is your cache it is the best solution for those inputs now, but this could change when you calculate the next item.
8.) Choose the correct statement(s) about event bubbling
  * A) As an event bubbles up, `this` always equals `event.target`
  * B) You cannot prevent an event from making its way all the way down to its target in the targeting phase; you must choose not to handle it once it arrives there
  * C) Events will reach every element that listens for them unless they fall outside the parent-child chain of the element on which the event occurred
  * D) Event delegation is useful when you might be dynamically adding children to a parent and you need to execute an action on the child
  * E) The properties of the event target are not available in other elements listening to the event unless they are explicitly attached to the event object
9.) Select the correct statement(s) about HTTP methods
  * A) POST requests cannot be bookmarked
  * B) GET requests can contain a body, but you should not expect it to have meaning to what is returned
  * C) PATCH requests are interpreted to replace only the specified fields
  * D) PUT requests that omit a field will update the resource b setting that field to null
10.) Choose the correct statement(s) about HTTPS
  * A) Successful Man in the Middle attacks can alter the request you are sending without your knowledge
  * B) Symmetric key exchange in the clear is sufficient to stop Man in the Middle attacks because the subsequent messages you send will be encrypted.
  * C) HTTPS relies on asymmetric key cryptography for encrypting the actual data you send in your request
  * D) Asymmetric Key exchange usually relies on a Certificate Authority to certify public keys
