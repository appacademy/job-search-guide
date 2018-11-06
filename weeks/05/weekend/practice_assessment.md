# 🚨 Practice Test 🚨 

Welcome to the end of Week 5! The next step is to double down on what you've learned, and prepare for the HackerRank test that will be in the following task. The first step is to work through this practice test to have an idea of what to expect on the HackerRank exam.

Before you dive into the HackerRank test, it's important to review. We use the HackerRank test results to gauge your progress in the job search guide, so you'll want to make sure you are as prepared as possible. If you struggle on this practice exam, be sure to review flash cards!

Make an honest effort with these problems. An answer key is at the bottom of the page, but try and review your notes and readings before referring to these. 

1. Choose the correct statement(s) about Binary Search
  * A) Binary Search always reduces the search space by half for each iteration/stach
  * B) The average Time Complexity is nlogn because you must consider every element and the stack has a height of log(n)
  * C) You can use a Binary Search algorithm to find peaks in dataset but you might not always know on which side of the current element a peak lies
  * D) You can use a Binary search any time you can determine from the current element which part of the dataset to search next
2. Which statement(s) about Promises is/are correct?
  * A) You must pass in your own Resolve and Reject functions as arguments to any Promise
  * B) XHR functions must be wrapped in a Promise in order to use the returned data in a function outside the scope of the XHR
  * C) The Resolve function does not take any arguments itself
  * D) `.then` takes two arguments, the first of which is required
  * E) `.catch` is the only way to handle the Reject case
  * F) `.then` executes the functions it is passed by placing them into the callback queue rather than directly on the execution stack
3. Choose the correct statement(s) about speeding up websites
  * A) Minifying files reduces load time by compressing data and mapping duplicated bytes
  * B) A CDN can reduce load times by speeding up the time it takes to resolve IP addresses
  * C) The order in which scripts are loaded affects the time it takes to load the DOM
  * D) Since images are loaded asynchronously anyway, it is best to load higher resolution images and scale them rather than having multiple copies on your server
  * E) You can control whether a client's browser should cache your assets for future reuse
4. Choose the correct statement(s) about Web Security
  * A) FTP is inherently safe because it is an encrypted protocol for transferring files
  * B) Session cookies are tied to the browser so exposing them over unencrypted channels poses a relatively small security risk
  * C) WPA2 provides end to end encryption over wireless network, so you don't have to use HTTPS to send secure traffic to the server
  * D) Public key cryptography ensure that the owner of the private key is the only one who can decrypt messages
  * E) In public key cryptography, messages you send to a receiver get encrypted with your public key
  * F) Certificate Authorities provide public keys that anyone can use to encrypt messages
  * G) Unsigned public keys can be used to perpetrate Man in the Middle attacks over HTTPS
  * H) Diffie-Hellman key exchange is used to establish symmetric encryption keys
  
5. Choose the correct statement(s) about searching algorithms
  * A) Interpolation search is a modified version of Binary Search
  * B) A rotated array can be searched using Binary Search, but it has a worse time complexity because first you have to find the pivot element, which takes linear time
  * C) Interpolation search has a worse worst case than Binary Search, but is useful for evenly distributed data sets
  * D) Interpolation search has a best case time complexity of log(n)^2 because you find the best element within each new subset to split the data on
6. Choose the correct statement(s) about Promises
  * A) `.then` returns the result of whichever of its function arguments is called
  * B) If the function that you pass to `.then` returns a promise, then the resolution of the `.then` will wait until the resolution of the Promise you created
  * C) Promise.resolve() wraps its argument in a Promise
  * D) Promise.resolve() must be explicitly called on any non-Promise arguments that are passed to Promise.all
  * E) Promise.all returns an array of promises in the order in which they are resolved
  * F) Promise.all will return a rejected promise if any of its arguments reject, even if some promises are still pending
  * G) You can only call .then on Promise.all if you can be sure that all of it's arguments will resolve
  * H) Promise.race will return a Promise with the same value as the first Promise to resolve, and thus all other Promises you pass it will remain pending
7. Choose the correct statement(s) about the DOM
  * A) Tags placed after the closing </body> tag won't be read by the browser
  * B) The DOM has only one root node
  * C) `.children` ignores text nodes
  * D) DOM collections returned by JS functions can be used to insert elements into the DOM by pushing onto the collection
  * E) The collections returned by JS functions that access the DOM are static, and will not increase in size if you later append the DOM.
8. Which of these statement(s) about algorithms is/are correct?
  * A) Finding the K-th smallest element is best solved using a min-heap
  * B) When using a max-heap to find the K-th smallest element, you have to have a heap of size n
  * C) finding the pair of elements in a sorted array that is closest to a given sum cannot be done in better than nlogn time
  * D) When finding the pair of elements in a sorted array that is closest to a given sum, you should track the best difference so far and use the current difference to decide which pointer to move
  * E) Quicksort has a worst case time complexity when there are more than 50% duplicate elements
  * F) In Quicksort, pathological datasets can be handled by randomizing the boundaries passed to the partition function
  * G) In an in-place implementation of Quicksort, a partition function is used to actually sort elements and sorts the entire array passed to it each iteration/stack
  * H) The return value of the partition function represents the index of an element in its final sorted location
9. Which statement(s) about async/await is/are correct?
  * A) async functions must take Promises as arguments
  * B) async function returns a Promise that resolves with the return value of the async function
  * C) async functions will only trigger .catch statements chained onto them if the async function throws an error
  * D) the `await` operator must precede a Promise expression
  * E) `await` can be used on the global scope
10. Select the correct statement(s) about OOP
  * A) Encapsulation refers to the idea that a class should represent one complete idea, and there should not be overlap with other classes
  * B) Getter and setter methods are used to access state from outside an object
  * C) Fields of an object refer to its internal state
  * D) Private methods can generally only be used by an instance of the class of the object and its parents
  * E) Classical inheritance involves defining that a class is a sub-type of another class, while class composition is building a class based on what it explicitly has and can do
  * F) Overriding inherited methods is a way to achieve polymorphism
  * G) It is possible to overload methods in Ruby, and the right method will be chosen based on the arguments signature
  * H) Dynamically typed languages check at compile-time whether an object can call a certain method
  * I) Classes are instances of an object in Ruby


---
## No Peeking!

* [Answer Key]('https://github.com/appacademy/job-search-guide/tree/master/weeks/05/weekend/answer_key.md')
