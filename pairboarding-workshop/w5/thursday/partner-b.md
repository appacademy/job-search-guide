# Partner B

## Time Management
* How do you manage your time and tasks?
* How do you stay organized?

## System Design
* Let's design Uber!

Note:
While designing a ride-sharing service, discuss things like:

* The most critical use case — when a customer requests a ride and how to efficiently match them with the nearby drivers?
* How to store millions of geographical locations for drivers and riders who are always moving.
* How to handle updates to driver/rider locations (millions of updates every second)?

## Longest Substring Without Duplication

Write a function that takes in a string and that returns its longest substring without duplicate characters.  Assume that there will only be one longest substring without duplication.

```
Sample Input: "clementisacap"
Sample Output: "mentisac"
```

### Answer
We can solve this problem efficiently by traversing the string and storing the last position at which we see each character in a hash table which we'll call `lastSeen`.  We'll also keep track of the `longest` string we've seen so far.  As we traverse the string we'll keep track of a variable called `startIdx` which will represent the most recent index from which we can start a substring with no duplicate characters, ending at the current index.  If we come across a character that we've already seen then we'll update our `startIdx` to be the maximum of the current `startIdx` and the position of the element the last time we saw it + 1.  Updating the `startIdx` in this way will make sure that we don't end up moving the `startIdx` backward when we encounter a duplicate character late in the string.  If the current string from the `startIdx` to the current position + 1 is greater than the length of the `longest` string we've seen so far, we'll update `longest` to the current string.

```JavaScript
function longestSubstringWithoutDuplication(string) {
  const lastSeen = {};
  // it's cheaper to just store the indices of the longest string seen so far
  // instead of the whole string
  let longest = [0, 1];
  let startIdx = 0;
  for (let i = 0; i < string.length; i++) {
    const char = string[i]
    if (lastSeen[char] !== undefined) {
      startIdx = Math.max(startIdx, lastSeen[char] + 1);
    }
    if (longest[1] - longest[0] < i + 1 - startIdx) {
      longest = [startIdx, i + 1];
    }
    lastSeen[char] = i;
  }
  return string.slice(longest[0], longest[1]);
}
```

The time complexity on the above solution is **O(n) & the space is O(min(n, a))** where n is the length of the string and a is the number of unique characters in the string.
