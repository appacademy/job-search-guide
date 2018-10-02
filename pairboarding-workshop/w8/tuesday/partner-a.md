# Partner A

## Tell me about a time
* Tell me about a time when you failed or weren’t successful?
* What was the result?

## JS Trivia
* What will the code below output to the console and why?

```JavaScript
(function(){
  var a = b = 3;
})();

console.log("a defined? " + (typeof a !== 'undefined'));
console.log("b defined? " + (typeof b !== 'undefined'));
```

## Answer
Since both `a` and `b` are defined within the enclosing scope of the function, and since the line they are on begins with the `var` keyword, most JavaScript developers would expect `typeof a` and `typeof b` to both be `undefined` in the above example.

However, that is not the case. The issue here is that most developers incorrectly understand the statement `var a = b = 3;` to be shorthand for:

```
var b = 3;
var a = b;
```

But in fact, `var a = b = 3;` is actually shorthand for:

```
b = 3;
var a = b;
```

As a result (if you are not using strict mode), the output of the code snippet would be:

```
a defined? false
b defined? true
```

But how can `b` be defined outside of the scope of the enclosing function? Well, since the statement `var a = b = 3;` is shorthand for the statements `b = 3;` and `var a = b;`, `b` ends up being a global variable (since it is not preceded by the `var` keyword) and is therefore still in scope even outside of the enclosing function.

Note that, in strict mode (i.e., with `"use strict"`), the statement `var a = b = 3;` will generate a runtime error of `ReferenceError: b is not defined`, thereby avoiding any headfakes/bugs that might otherwise result. (Yet another prime example of why you should use `use strict` as a matter of course in your code!)

## Maximum Subset Sum With No Adjacent Elements
* Write a function that takes in an array of positive integers and returns an integer representing the maximum sum of non-adjacent elements in the array.  If a sum cannot be generated, the function should return 0.

Example:
```
input: [75, 105, 120, 75, 90, 135]
output: 330 // (75 + 120 + 135)
```

### Answer
We can solve this problem efficiently by using dynamic programming.  What we'll do is solve smaller versions of the problem to build up our solution.  To start, we'll create an array that is the same length as our input array, and at each index we'll store the greatest sum that we can generate using no adjacent numbers up until and including the index in which we're storing that sum.  For example if our input was `[7, 10, 12, 7, 9, 14]` then our resulting array would be `[7, 10, 19, 19, 28, 33]`.  So now the question becomes, is there a pattern or formula that we can derive to determine how to calculate the next value in our result array based on the previous value and the input array.  The answer, of course, is yes there is.  Let's consider how we would find the final value `33` in our result array.  So far our result is `[7, 10, 19, 19, 28, ??]` and the way we can determine what the next value is with this formula: `result[i] = max(result[i - 1], result[i - 2] + input[i])`.  You can convince yourself that this formula works by applying it to the result array in example above for any input where `i` is greater than 2.  Once our result array is built up we simply return the last value in it.  The time complexity of this solution is O(n) and the space is O(n).

```JavaScript
const maxSubsetSumNoAdjacent = (arr) => {
  if (arr.length === 0) return 0;
  if (arr.length === 1) return arr[0];
  const maxSums = arr.slice();
  maxSums[1] = Math.max(arr[0], arr[1]);
  for (let i = 2; i < arr.length; i++) {
    maxSums[i] = Math.max(maxSums[i - 1], maxSums[i - 2] + arr[i]);
  }
  return maxSums[maxSums.length - 1]
}
```

We can do slightly better than this solution, however.  If you look at what we actually need for our solution we only need to keep track of a pointer to `i - 1` and `i - 2` instead of storing the entire result array.  This will reduce our space complexity to O(1).

```JavaScript
const maxSubsetSumNoAdjacent = (arr) => {
  if (arr.length === 0) return 0;
  if (arr.length === 1) return arr[0];
  let second = arr[0];
  let first = Math.max(arr[0], arr[1]);
  for (let i = 2; i < arr.length; i++) {
    const curr = Math.max(maxSums[i - 1], maxSums[i - 2] + arr[i]);
    second = first;
    first = curr;
  }
  return first;
}
```
