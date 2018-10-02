# Partner B

## Behavioral
* Have you ever had to deal with features that involved multiple people working in the same areas?
* How did it go?
* Was there anything that could have been done to improve it?

## JS Trivia
* What will be the output when the following code is executed? Explain.

```JavaScript
console.log(false == '0')
console.log(false === '0')
```

The code will output:

```
true
false
```

In JavaScript, there are two sets of equality operators. The triple-equal operator `===` behaves like any traditional equality operator would: evaluates to true if the two expressions on either of its sides have the same type and the same value. The double-equal operator, however, tries to coerce the values before comparing them. It is therefore generally good practice to use the `===` rather than `==`. The same holds true for `!==` vs `!=`.

## Levenshtein Distance
Write a function that takes in two strings and returns the minimum number of edit operations that need to be performed on the first string to obtain the second string.  There are three edit operations: insertion of a character, deletion of a character, and substitution of a character for another.

```
input: "abc", "yabd"
output: 2 // (insert "y"; substitute "c" for "d")
```

### Answer
We can solve this problem efficiently using dynamic programming.  We'll start by building up a 2d array, hereby referred to as `edits`, of the minimum numbers of edits for pairs of substrings of the input strings.  The rows of the array represent substrings of the second input string `str2`.  The first row represents the empty string and each row `i` thereafter represents the substrings of `str2` from `0` to `i`, with `i` excluded.  The columns will similarly represent the first input string `str1`.  See example below:

```
str1 = "abc"
str2 = "yabd"

   "" a, b, c
"" 0  1  2  3
y  1  1  2  3
a  2  1  2  3
b  3  2  1  2
d  4  ?  ?  ?
```
To fill in the above grid we'll go one row at a time.  We'll find the minimum numbers of edits between all the substrings of str1 represented by the columns and the empty string represented by the first row, then between all the substrings of `str1` represented by the columns and the first letter of `str2` represented by the second row, etc., until we compare both full strings.  Now we can derive a formula for for finding the next value in our 2d array based on the previous values in our array.  Our formula is as follows:
```
if (str1[i] == str2[j]) edits[i][j] = edits[i - 1][j - 1]
else edits[i][j] = 1 + min(edits[i][j - 1], edits[i - 1][j], edits[i - 1][j - 1])
```

Finally at the end we return the last value in our edits array.  See code implementation below.

```JavaScript
const levenshteinDistance = (str1, str2) => {
  // build up first row and col of 2d array
  const edits = [];
  for (let i = 0; i < str2.length + 1; i++) {
    const row = [];
    for (let j = 0; j < str1.length + 1; j++) {
      row.push(j)
    }
    row[0] = i;
    edits.push(row);
  }
  for (let i = 1; i < str2.length + 1; i++) {
    for (let j = 1; j < str1[j - 1]) {
      if (str2[i - 1] === str1[j - 1]) {
        edits[i][j] = edits[i - 1][j - 1];
      } else {
        edits[i][j] = 1 + Math.min(edits[i - 1][j - 1], edits[i - 1][j], edits[i][j - 1]);
      }
    }
  }
  return edits[str2.length][str1.length]
}
```

The above solution is okay; it has a time & space complexity of O(nm), but we can do better.  If you notice, we only ever need to hold on to two rows of our 2d array in memory at any given time because we only check the previous row to figure out the next value.  Below is an optimized solution where we only ever store two rows of our 2d array at one time.  It has a space complexity O(min(n, m)) where n & m are the length of str1 and str2 respectively.

```JavaScript
const levenshteinDistance = (str1, str2) => {
  const small = str1.length < str2.length ? str1 : str2;
  const big = str1.length >= str2.length ? str1 : str2;
  const evenEdits = [];
  const oddEdits = new Array(small.length + 1);
  for (let j = 0; j < small.length + 1; j++) {
    evenEdits.push(j);
  }
  for (let i = 1; i < big.length + 1; i++) {
    let currentEdits, previousEdits;
    if (i % 2 === 1) {
      currentEdits = oddEdits;
      previousEdits = evenEdits;
    } else {
      currentEdits = evenEdits;
      previousEdits = oddEdits;
    }
    currentEdits[0] = i;
    for (let j = 1; j < small.length + 1; j++) {
      if (big[i - 1] === small[j - 1]) {
        currentEdits[j] = previousEdits[j - 1];
      } else {
        currentEdits[j] = 1 + Math.min(previousEdits[j - 1], previousEdits[j], currentEdits[j - 1]);
      }
    }
  }
  return big.length % 2 === 0 ? evenEdits[small.length] : oddEdits[small.length];
}
