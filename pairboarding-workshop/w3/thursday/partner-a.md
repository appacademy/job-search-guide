# Partner A

## Being a Team Player
* Walk me through a recent team project you worked on?  
* What were the results?  
* What worked well?  
* What could have been improved?

## Stack Overflow
* The following recursive code will cause a stack overflow if the array list is too large.  How can you fix this and still retain the recursive pattern?

```JavaScript
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};
```

### Answer
The potential stack overflow can be avoided by modifying the nextListItem function as follows:

```JavaScript
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        setTimeout( nextListItem, 0);
    }
};
```

The stack overflow is eliminated because the event loop handles the recursion, not the call stack. When ```nextListItem``` runs, if ```item``` is not null, the timeout function (```nextListItem```) is pushed to the event queue and the function exits, thereby leaving the call stack clear. When the event queue runs its timed-out event, the next item is processed and a timer is set to again invoke ```nextListItem```. Accordingly, the method is processed from start to finish without a direct recursive call, so the call stack remains clear, regardless of the number of iterations.

## Determine if an Array represents a min heap or not
* Given an array of integers determine if it represents a min heap or not.  Return ```true``` if it does and ```false``` if it doesn't.

```JavaScript
let heapA = [2,3,2,11,4,7,4]
let heapB = [2,3,1,11,4,7,4]

isMinHeap(heapA) // true
isMinHeap(heapB) // false
```

### Answer
Since the input is an array, we know that the **structural property of the heap** (all levels except the last level are full) cannot be violated.  We only have to worry about the **Min-Heap Property** (value of a node is at least as large as that of its parent) for the given problem.

Since array indexing begins from 0, for a given array index i, if (2*i + 2 > n) is true then A[i] represents a leaf node.  Otherwise, when (2*i + 2 <= n) is true, A[i] represents an internal heap node.  Here n is the size of the array.

Now that we know how to differentiate between a leaf node and an internal based on a given array index and number of nodes, lets circle back to the problem.

We can efficiently solve this problem by using recursion.  The idea is to start from the root node (at index 0) and check if the left and right child (if any) of the root node is greater than the root node or not.  If yes, we recursively call the function for both its children, else we return false from the function.

```JavaScript
// idx is initially set to zero (root of the heap)
const isMinHeap = (heapArr, idx = 0) => {
  // if idx is a leaf node return true as every leaf node is a heap
  if (2 * idx + 2 > heapArr.length) return true;

  // otherwise we know idx is an internal node
  // recursively check if left child is a heap
  let left = heapArr[idx] <= heapArr[2 * idx + 1] && isMinHeap(heapArr, 2 * idx + 1);

  // recursively check if right child is a heap (to avoid array out of bounds we first check if a right child exists or not)
  let right = (2 * idx + 2 === heapArr.length) ||
    heapArr[idx] <= heapArr[2 * idx + 2] && isMinHeap(heapArr, 2 * idx + 2);

  // return true if both left and right children are heaps
  return left && right;
}

let heapA = [2,3,2,11,4,7,4]
let heapB = [2,3,1,11,4,7,4]

isMinHeap(heapA) // true
isMinHeap(heapB) // false
```
