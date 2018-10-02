# Partner B

## Dead Weight
* Have you ever had to work with someone else that didn’t pull their weight on a project?
* How did you handle it?
* Did things ever improve?
* If you had to do it all over again would you change anything?

## So strict!
* What is the significance, and what are the benefits, of including ```'use strict'``` at the beginning of a JavaScript source file?

### Answer
* The short and most important answer here is that ```'use strict'``` is a way to voluntarily enforce stricter parsing and error handling on your JavaScript code at runtime. Code errors that would otherwise have been ignored or would have failed silently will now generate errors or throw exceptions. In general, it is a good practice.

## Iterative Quicksort
* Implement an iterative version of the Quicksort algorithm

```JavaScript
let a = [9, -3, 5, 2, 6, 8, -6, 1, 3];
quicksort(a); // [ -6, -3, 1, 2, 3, 5, 6, 8, 9 ]
```

### Answer
* The idea is to use a stack for storing sub-array starting & ending indices and for later processing instead of using recursion.  Note that the partitioning logic remains the same.

```JavaScript
class QuickSort {
    swap(arr, i, j) {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    partition(arr, start, end) {
        // Pick rightmost element as pivot from the array
        let pivot = arr[end];

        // elements less than pivot will go to the left of pIndex
        // elements more than pivot will go to the right of pIndex
        // equal elements can go either way
        let pIndex = start;

        // each time we finds an element less than or equal to pivot,
        // pIndex is incremented and that element would be placed
        // before the pivot.
        for (let i = start; i < end; i++) {
            if (arr[i] <= pivot) {
                this.swap(a, i, pIndex);
                pIndex++;
            }
        }
        // swap pIndex with Pivot
        this.swap (a, pIndex, end);

        // return pIndex (index of pivot element)
        return pIndex;
    }

    // Iterative Quicksort routine
    iterativeQuickSort(arr) {
        // stack of pairs for storing subarray start and end index
        let stack = [];

        // get starting and ending index of given array (vector)
        let start = 0;
        let end = a.length - 1;

        // push array start and end index to the stack
        stack.push([start, end]);

        // run till stack is not empty
        while (stack.length > 0) {
            // pop top pair from the list and get sub-array starting
            // and ending indices
            let curr = stack.pop();
            start = curr[0];
            end = curr[1];

            // rearrange the elements across pivot
            let pivot = this.partition(a, start, end);

            // push sub-array indices containing elements that are
            // less than current pivot to stack
            if (pivot - 1 > start) {
                stack.push([start, pivot - 1]);
            }

            // push sub-array indices containing elements that are
            // more than current pivot to stack
            if (pivot + 1 < end) {
                stack.push([pivot + 1, end]);
            }
        }
        return arr;
    }
}
let a = [9, -3, 5, 2, 6, 8, -6, 1, 3]
let QS = new QuickSort();
QS.iterativeQuickSort(a) // returns => [-6, -3, 1, 2, 3, 5, 6, 8, 9]
```
