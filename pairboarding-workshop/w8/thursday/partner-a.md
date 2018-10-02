# Partner A

## Dev Cycles
* We are in the middle of a development cycle (or sprint if you use agile) and there is a major change in the functionality of a feature you have been working on.
* How do you respond?
* What questions do you ask?

## Cloning
* How do you clone and object in JS?

### Answer
```javascript
var obj = {a: 1 ,b: 2}
var objclone = Object.assign({},obj);
```

Now the value of objclone is `{a: 1 ,b: 2}` but points to a different object than `obj`.

Note the potential pitfall, though: `Object.clone()` will just do a shallow copy, not a deep copy. This means that nested objects aren’t copied. They still refer to the same nested objects as the original:

```javascript
let obj = {
    a: 1,
    b: 2,
    c: {
        age: 30
    }
};

var objclone = Object.assign({},obj);
console.log('objclone: ', objclone);

obj.c.age = 45;
console.log('After Change - obj: ', obj);           // 45 - This also changes
console.log('After Change - objclone: ', objclone); // 45
```

## Min Number of Coins to Make Change
Write a function that takes in an amount and a set of coins.  Return the minimum number of coins needed to make change for the given amount.  You may assume you have an unlimited supply of each type of coin. If it's not possible to make change for a given amount, return nil or NaN.

Example:
``` ruby
make_change(14, [10, 7, 1])
# return 2 because [7, 7] is the smallest combination
```

## Solution

### Brute Force Iterative
```ruby
def make_change(amount, coins = [25, 10, 5, 1])
  coins = coins.sort.reverse

  best_change = nil

  (0...coins.count).each do |index|
    change = []
    total = 0
    coins.drop(index).each do |coin|
      until (coin + total) > amount
        change << coin    
        total += coin
      end
    end

    if (best_change.nil? || change.count < best_change.count)
      best_change = change
    end
  end

  return best_change if best_change.nil?
  best_change.count
end
```

### Dynamic Programming

```JavaScript
const makeChange = (n, coins) {
  const numOfCoins = (new Array(n + 1)).fill(Infinity);
  numOfCoins[0] = 0;
  for (let coin in coins) {
    for (let amount = 0; amount < numOfCoins.length; amount++) {
      if (coin <= amount) {
        numOfCoins[amount] = Math.min(numOfCoins[amount], numOfCoins[amount - coin] + 1);
      }
    }
  }
  return numOfCoins[n] !== Infinity ? numOfCoins[n] : NaN;
}
```

## Detailed Explanation of mutliple approaches (highly recommended)

https://leetcode.com/articles/coin-change/
