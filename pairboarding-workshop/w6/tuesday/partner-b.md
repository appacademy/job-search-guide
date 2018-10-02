# Partner B

## Behavioral
* What is the best way to collaborate on a coding project?

## Integral Integers
* Discuss possible ways to write a function `isInteger(x)` that determines if `x` is an integer.

### Answer
This may sound trivial and, in fact, it is trivial with ECMAscript 6 which introduces a new `Number.isInteger()` function for precisely this purpose. However, prior to ECMAScript 6, this is a bit more complicated, since no equivalent of the `Number.isInteger()` method is provided.

The issue is that, in the ECMAScript specification, integers only exist conceptually; i.e., numeric values are always stored as floating point values.

With that in mind, the simplest and cleanest pre-ECMAScript-6 solution (which is also sufficiently robust to return `false` even if a non-numeric value such as a string or `null` is passed to the function) would be the following use of the bitwise XOR operator:

```JavaScript
function isInteger(x) { return (x ^ 0) === x; }
```

The following solution would also work, although not as elegant as the one above:

```JavaScript
function isInteger(x) { return Math.round(x) === x; }
```

Note that `Math.ceil()` or `Math.floor()` could be used equally well (instead of `Math.round()`) in the above implementation.

Or alternatively:

```JavaScript
function isInteger(x) { return (typeof x === 'number') && (x % 1 === 0); }
```

One fairly common incorrect solution is the following:

```JavaScript
function isInteger(x) { return parseInt(x, 10) === x; }
```

While this `parseInt`-based approach will work well for many values of x, once x becomes quite large, it will fail to work properly. The problem is that `parseInt()` coerces its first parameter to a string before parsing digits. Therefore, once the number becomes sufficiently large, its string representation will be presented in exponential form (e.g., `1e+21`). Accordingly, `parseInt()` will then try to parse `1e+21`, but will stop parsing when it reaches the `e` character and will therefore return a value of 1. Observe:

```JavaScript
> String(1000000000000000000000)
'1e+21'
> parseInt(1000000000000000000000, 10)
1
> parseInt(1000000000000000000000, 10) === 1000000000000000000000
false
```

## Boggle Board ([From Geeks For Geeks](https://www.geeksforgeeks.org/boggle-find-possible-words-board-characters/))
Given a dictionary and an M x N board where every node has one character. Find all possible words that can be formed by a sequence of adjacent characters. Note that we can move to any of 8 adjacent characters, but a word should not have multiple instances of the same node.  

Example:
```JavaScript
// Input:
let dictionary = ["GEEKS", "FOR", "QUIZ", "GO"];
let boggle = [['G','I','Z'],
              ['U','E','K'],
              ['Q','S','E']];
findWords(boggle) // => The Following words of dictionary are present
                  // => GEEKS
                  // => QUIZ
```

### Answer
The idea is to consider every character as a starting character and to then find all words starting with it. All words starting from a character can be found using Depth First Search. We do a depth first traversal starting from every node and keep track of visited nodes to make sure that a node is only considered once in a word.
Note that this is a naive approach, you can read more about the optimized approach [here](https://www.geeksforgeeks.org/boggle-set-2-using-trie/).

```JavaScript
// Let the given dictionary be following
let dictionary = ["GEEKS", "FOR", "QUIZ", "GO"];

const isWord = (str) => {
	// Linearly search all words
	for (let i = 0; i < dictionary.length; i++) {
    if (str == dictionary[i]) return true;
  }		
	return false;
}

// A recursive function to print all words present on boggle
const findWordsUtil = (boggle, visited, i, j, str) => {
	// Mark current node as visited and append current character
	// to str
	visited[i][j] = true;
	str = str + boggle[i][j];

	// If str is present in dictionary, then print it
	if (isWord(str) === true)
		console.log(str);

	// Traverse 8 adjacent nodes of boggle[i][j]
	for (let row = i - 1; row <= i + 1 && row < boggle.length; row++) {
    for (let col = j - 1; col <= j + 1 && col < boggle[i].length; col++) {
      if (row >= 0 && col >= 0 && !visited[row][col]) {
        findWordsUtil(boggle, visited, row, col, str);
      }
    }

  }
	// Erase current character from string and mark visited
	// of current node as false
	let strArr = str.split("")
  strArr.pop()
  str = strArr.join("");
	visited[i][j] = false;
}

// Prints all words present in dictionary.
const findWords = (boggle) => {
	// Mark all characters as not visited
	let visited = boggle.map(row => row.map(value => false));;

	// Initialize current string
	let str = "";

	// Consider every character and look for all words
	// starting with this character
	for (let i=0; i < boggle.length; i++) {
    for (let j = 0; j < boggle[i].length; j++) {
      findWordsUtil(boggle, visited, i, j, str);
    }		
  }
}

let boggle = [['G','I','Z'],
					['U','E','K'],
					['Q','S','E']];

console.log("The following words of dictionary are present");

findWords(boggle); // prints => 'GEEKS', 'QUIZ'
```
Note that the above solution may print the same word multiple times. For example, if we add “SEEK” to the dictionary, it is printed multiple times. To avoid this, we can use hashing to keep track of all printed words.
