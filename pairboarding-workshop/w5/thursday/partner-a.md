# Partner A

## Behavioral
* What do you like about software/tech?

## Apply yourself
* How could you use Math.max to find the maximum value in an array?

### Answer
Use apply on Math.max and pass the array as apply takes an array of arguments. Since we are not reading anything from this or using it at all. We can simply pass null as first parameter.

```JavaScript
function getMax(arr){
  return Math.max.apply(null, arr);  
}
```

## Min Number Of Jumps
You are given a non-empty array of integers. Each element represents the maximum number of steps you can take forward. For example, if the element at index 1 is 3, you can go from index 1 to index 2, 3, or 4. Write a function that returns the minimum number of jumps needed to reach the final index. Note that jumping from index i to index i + x always constitutes 1 jump, no matter how large x is.
​
```
Sample input: [3, 4, 2, 1, 2, 3, 7, 1, 1, 1, 3]
Sample output: 4 // (3 --> 4 or 2 --> 2 or 3 --> 7 --> 3)
```

### Answer
The naive approach to solve this problem is to build an array that holds the minimum number of jumps needed to go from index 0 to all indices.  Start at index 0 and progressively build up the array, using previously calculated values to find the next ones.

```JavaScript
function minNumberOfJumps(array) {
  const jumps = (new Array(array.length)).fill(Infinity);
  jumps[0] = 0;
  for (let i = 1; i < array.length; i++) {
    for (let j = 0; j < i; j++) {
      if (array[j] >= i - j) {
        jumps[i] = Math.min(jumps[j] + 1, jumps[i]);
      }
    }
  }
  return jumps[jumps.length - 1];
}
// O(n^2) time & O(n) space
```
Building the array in the above solution is okay but we can reach a more optimized solution by realizing that at any point in the array we know the farthest index that you can reach (`maxReach`) as well as the number of steps that you you have left until you must "consume" a jump.  We'll traverse the array and update our `maxReach` as we go by taking the max of the existing `maxReach` and the value we're at in the input array plus the index that we're at.  As we iterate we'll decrement our `steps` by one each time, because moving from one index to the next uses up one step.  When our `steps` reach zero, we increment `jumps` by one, because at that point we are forced to jump to continue iterating and we'll recalculate our steps by taking the current `maxReach` and subtracting the current index we're on from it.  This will give us a time complexity of O(n) & a space complexity of O(1).


```JavaScript
function minNumberOfJumps(array) {
	if (array.length === 1) return 0;
	let jumps = 0;
	let maxReach = array[0];
	let steps = array[0];
	for (let i = 1; i < array.length - 1; i++) {
		maxReach = Math.max(maxReach, i + array[i]);
		steps -= 1;
		if (steps === 0) {
			jumps += 1;
			steps = maxReach - i
		}
	}
	return jumps + 1
}
```
