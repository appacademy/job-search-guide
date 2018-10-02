# Partner B

## Culture Fit
* There are many types of company cultures...what type of culture is important to you?
* What are ways you develop relationships with collaborators/team mates?

## You get a pass
* Does JavaScript pass by value or by reference?

### Answer
* Primitive types (strings, numbers, etc.) are passed by value & objects are passed by reference.  If you change the properties of the passed object, the change will be affected.  However, if you assign a new object to the passed object, the changes will not be reflected.  You can read more about it [here](https://snook.ca/archives/javascript/javascript_pass).

```JavaScript
var num = 10,
    name = "Addy Osmani",
    obj1 = {
      value: "first value"
    },
    obj2 = {
     value: "second value"
    },
    obj3 = obj2;

function change(num, name, obj1, obj2) {
    num = num * 10;
    name = "Paul Irish";
    obj1 = obj2;
    obj2.value = "new value";
}

change(num, name, obj1, obj2);

console.log(num); // 10
console.log(name);// "Addy Osmani"
console.log(obj1.value);//"first value"
console.log(obj2.value);//"new value"
console.log(obj3.value);//"new value"        
```

## Convert Min-heap to Max-heap in O(n) time
* Given an array representing a min-heap, convert the min-heap to a max-heap.  The conversion should be done in-place an in linear time.

### Answer
The idea is inspired from the HeapSort algorithm.  The problem looks complex at first glance but this problem is no different than building a max-heap from an unsorted array.  In other words, it doesn't matter if this is a min-heap or not.  We can simply build the max-heap from the given array by starting from the last internal node (right-most, bottom-most node) of the min-heap and heapifying all internal nodes in a bottom-up manner to build the max-heap.

```JavaScript
// data structure for Min Heap
class ConvertHeap {
    // return left child of arr[i]
    left (i) {
        return (2 * i + 1);
    }

    // return right child of arr[i]
    right(i) {
        return (2 * i + 2);
    }

    // Utility function to swap two indices in the array
    swap(arr, i, j) {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // recursive heapifyDown algorithm. The node at index i and
    // its two direct children violate the heap property
    heapifyDown(arr, i, size) {
        // get left and right child of node at index i
        let left = this.left(i);
        let right = this.right(i);

        let smallest = i;

        // compare arr[i] with its left and right child
        // and find smallest value
        if (left < size && arr[left] < arr[i]) {
            smallest = left;
        }

        if (right < size && arr[right] < arr[smallest]) {
            smallest = right;
        }

        // swap with child having lesser value and
        // call heapify-down on the child
        if (smallest !== i) {
            this.swap(arr, i, smallest);
            this.heapifyDown(arr, smallest, size);
        }
    }

    // build heap
    convert(arr) {
        // call heapifyDown starting from last internal node all the
        // way upto the root node
        let i = Math.floor((arr.length - 2) / 2);
        while (i >= 0) {
            this.heapifyDown(arr, i--, arr.length);
        }
        return arr;
    }

}
/*
            9

      4         7

    1   -2   6      5

*/
// array representing max heap
let arr = [ 9, 4, 7, 1, -2, 6, 5 ];

// build a min heap by initializing it by given array
let converter = new ConvertHeap();
converter.convert(arr); // => [ -2, 1, 5, 9, 4, 6, 7 ]
// print the Min Heap
/*
        -2

    1         5

9     4   6     7     */
```
