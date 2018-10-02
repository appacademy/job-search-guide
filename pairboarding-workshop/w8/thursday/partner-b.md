# Partner B

## Improvements
* Tell me about a time you improved a tool, task, or project you were working on. What was the circumstances?
* Why did you do it?  
* Do you have any other examples?

## JS Trivia
* What do the following lines output, and why?

```JavaScript
console.log(1 < 2 < 3);
console.log(3 > 2 > 1);
```

The first statement returns `true` which is as expected.

The second returns `false` because of how the engine works regarding operator associativity for `<` and `>`. It compares left to right, so `3 > 2 > 1` JavaScript translates to `true > 1`. `true` has value `1`, so it then compares `1 > 1`, which is `false`.

## Number of ways to Make Change
Given an array of positive integers representing coin denominations and a single non-negative integer representing a target amount of money, implement a function that returns the number of ways to make change for that target amount using the given coin denominations.  Note that an unlimited number of coins is at your disposal.

```
input: 6, [1, 5]
output: 2 // (1x1 + 1x5 and 6x1)
```

### Answer
If you haven't noticed a theme yet this week, we can solve this problem with dynamic programming.  We'll start by building up an array of the number of ways to make change for all amounts between `0` and `n` inclusive (hereby referred to as `ways`).  Once we've built this array we'll again look to derive a formula to determine the next value in our array based on the previous values in our array and the array that makes up our coin denominations.  Our formula is:

```
if denom < amount:
  ways[amount] += ways[amount - denom]
```

The following implementation is O(nd) for time complexity where d is the number of denominations and the space complexity is O(n).

```JavaScript
const numberOfWaysToMakeChange = (n, denoms) => {
  const ways = (new Array(n + 1)).fill(0);
  ways[0] = 1;
  for (let denom of denoms) {
    for (let amount = 1; amount < n + 1; amount++) {
      if (denom <= amount) {
        ways[amount] += ways[amount - denom];
      }
    }
  }
  return ways[n];
}
```
