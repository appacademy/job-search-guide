# Partner A

## Under Pressure
* Walk me through a situation where you were under significant pressure to deliver a project on time.
* What was at stake?
* What — if anything — did you need to do/change to make the deadline?


## But you promised!
* What are promises and how are they useful?

### Answer
We use promises for handling asynchronous interactions in a sequential manner. They are especially useful when we need to do an async operation and THEN do another async operation based on the results of the first one. For example, if you want to request the list of all flights and then for each flight you want to request some details about it. The promise represents the future value. It has an internal state (pending, fulfilled and rejected) and works like a state machine.

A promise object has then method, where you can specify what to do when the promise is fulfilled or rejected.

You can chain then() blocks, thus avoiding the callback hell. You can handle errors in the catch() block. After a promise is set to fulfilled or rejected state, it becomes immutable.



## In-place merge two sorted arrays

* Given two sorted arrays of size m & n, merge the elements of the first array with the second array by maintaining the sorted order.  i.e. fill the first array with with the first m smallest elements and fill the second array with the remaining n elements.

### Answer
The idea is very simple.  We consider each element of array1 and ignore the element if it is already in correct order (i.e. the element smallest among all remaining elements) else we swap it with the smallest element which happens to be the first element of array2.  After swapping, we move the element (now present at ```array2[0]```) to its correct position in array2 to maintain the sorted order.  The merge process is similar to the merge routine of mergesort minus the auxiliary array for merging.

```JavaScript
// in-place merge two sorted arrays
//
const merge = (arr1, arr2) => {
    let arr1Length = arr1.length;
    let arr2Length = arr2.length;
    for (let i = 0; i < arr1Length; i++) {
      if (arr1[i] > arr2[0]) {
        [arr1[i], arr2[0]] = [arr2[0], arr1[i]];
        let first = arr2[0];
        let j;
        for (j = 1; j < arr2Length && arr2[j] < first; j++) {
          arr2[j - 1] = arr2[j];
        }
        arr2[j - 1] = first
      }
    }
}

let arr1 = [1, 4, 7, 8, 10];
let arr2 = [2, 3, 9]

console.log(arr1, arr2)
merge(arr1, arr2)
console.log(arr1, arr2)
```
* The above solution is O(mn) time complexity and O(1) space complexity.  This problem can in fact be solved in linear time and constant space.  Read up more on the approach [here](http://www.akira.ruc.dk/~keld/teaching/algoritmedesign_f04/Artikler/04/Huang88.pdf).
