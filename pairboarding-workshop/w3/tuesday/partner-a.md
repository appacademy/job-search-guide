# Partner A

## Feeling Conflicted
* Tell me about a conflict you had with another team member.
* What caused it?  What did you do?
* What’s the status of that relationship now?

## Equality
* How would you compare two objects in JavaScript?

### Answer
JavaScript has two different approaches for testing equality. Primitives like strings and numbers are compared by their value, while objects like arrays, dates, and user defined objects are compared by their reference. This means it compares whether two objects are referring to the same location in memory.

Equality check will check whether two objects have same value for same property. To check that, you can get the keys for both the objects. If the number of properties doesn't match, these two objects are not equal. Secondly, you will check each property whether they have the same value. If all the properties have same value, they are equal.

```JavaScript
function isEqual(a, b) {
    var aProps = Object.getOwnPropertyNames(a),
        bProps = Object.getOwnPropertyNames(b);

    if (aProps.length != bProps.length) {
        return false;
    }

    for (var i = 0; i < aProps.length; i++) {
        var propName = aProps[i];

        if (a[propName] !== b[propName]) {
            return false;
        }
    }
    return true;
}
```

## Merge M Sorted Lists of Variable Length
* Given an array of sorted integer arrays, print them in sorted order efficiently.  The number of arrays in your array of arrays can vary as can the length of each individual array.

```JavaScript
let list = [
        [10, 20, 30, 40],
        [15, 25, 35],
        [27, 29, 37, 48, 93],
        [32, 33]
      ]
printSorted(list); // => [ 10, 15, 20, 25, 27, 29, 30, 32, 33, 35, 37, 40, 48, 93 ]
```

### Answer
A simple solution would be to create an auxiliary array containing all elements of all lists (order doesn't matter).  Then we use an efficient sorting algorithm to sort the array in ascending order and print the elements.  The worst case time complexity of this approach will be O(Nlog(N)) where N is the total number of elements present in all lists.  **This approach is okay but we can do better!**

We can efficiently solve this problem in O(N(log(M))), where M is the total number of subarrays in our array of arrays, by using a min-heap.  The idea is to construct a min-heap of size M and insert the first element of each list item into it.  Then we pop the root element (the minimum in a min-heap) from the heap and insert the next element from the same list as the popped element.  We repeat until the heap is exhausted.  Finally we store the popped element in in an auxiliary array called ```result``` and return it at the end.

```JavaScript

// helper class to let us compare two nodes to each other
class Comparator {
  /**
   * @param {function(a: *, b: *)} [compareFunction]
   */
  constructor(compareFunction) {
    this.compare = Comparator.defaultCompareFunction;
    this.compare = this.compare.bind(this);
  }

  /**
   * @param {(string|number)} a
   * @param {(string|number)} b
   * @returns {number}
   */
  static defaultCompareFunction(a, b) {
    if (a.value === b.value) {
      return 0;
    }

    return a.value < b.value ? -1 : 1;
  }

  equal(a, b) {
    return this.compare(a, b) === 0;
  }

  lessThan(a, b) {
    return this.compare(a, b) < 0;
  }

  greaterThan(a, b) {
    return this.compare(a, b) > 0;
  }

  lessThanOrEqual(a, b) {
    return this.lessThan(a, b) || this.equal(a, b);
  }

  greaterThanOrEqual(a, b) {
    return this.greaterThan(a, b) || this.equal(a, b);
  }

  reverse() {
    const compareOriginal = this.compare;
    this.compare = (a, b) => compareOriginal(b, a);
  }
}

// definition for heap node
class MinHeap {
  /**
   * @param {Function} [comparatorFunction]
   */
  constructor(comparatorFunction) {
    // Array representation of the heap.
    this.heapContainer = [];
    this.compare = new Comparator(comparatorFunction);
    this.length = 0;
  }

  /**
   * @param {number} parentIndex
   * @return {number}
   */
  getLeftChildIndex(parentIndex) {
    return (2 * parentIndex) + 1;
  }

  /**
   * @param {number} parentIndex
   * @return {number}
   */
  getRightChildIndex(parentIndex) {
    return (2 * parentIndex) + 2;
  }

  /**
   * @param {number} childIndex
   * @return {number}
   */
  getParentIndex(childIndex) {
    return Math.floor((childIndex - 1) / 2);
  }

  /**
   * @param {number} childIndex
   * @return {boolean}
   */
  hasParent(childIndex) {
    return this.getParentIndex(childIndex) >= 0;
  }

  /**
   * @param {number} parentIndex
   * @return {boolean}
   */
  hasLeftChild(parentIndex) {
    return this.getLeftChildIndex(parentIndex) < this.heapContainer.length;
  }

  /**
   * @param {number} parentIndex
   * @return {boolean}
   */
  hasRightChild(parentIndex) {
    return this.getRightChildIndex(parentIndex) < this.heapContainer.length;
  }

  /**
   * @param {number} parentIndex
   * @return {*}
   */
  leftChild(parentIndex) {
    return this.heapContainer[this.getLeftChildIndex(parentIndex)];
  }

  /**
   * @param {number} parentIndex
   * @return {*}
   */
  rightChild(parentIndex) {
    return this.heapContainer[this.getRightChildIndex(parentIndex)];
  }

  /**
   * @param {number} childIndex
   * @return {*}
   */
  parent(childIndex) {
    return this.heapContainer[this.getParentIndex(childIndex)];
  }

  /**
   * @param {number} indexOne
   * @param {number} indexTwo
   */
  swap(indexOne, indexTwo) {
    const tmp = this.heapContainer[indexTwo];
    this.heapContainer[indexTwo] = this.heapContainer[indexOne];
    this.heapContainer[indexOne] = tmp;
  }

  /**
   * @return {*}
   */
  peek() {
    if (this.heapContainer.length === 0) {
      return null;
    }

    return this.heapContainer[0];
  }

  /**
   * @return {*}
   */
  poll() {
    if (this.heapContainer.length === 0) {
      return null;
    }

    if (this.heapContainer.length === 1) {
      this.length -= 1;
      return this.heapContainer.pop();
    }

    const item = this.heapContainer[0];

    // Move the last element from the end to the head.
    this.heapContainer[0] = this.heapContainer.pop();
    this.heapifyDown();
    this.length -= 1;
    return item;
  }

  /**
   * @param {*} item
   * @return {MinHeap}
   */
  add(item) {
    this.heapContainer.push(item);
    this.heapifyUp();
    this.length += 1;
    return this;
  }

  /**
   * @param {*} item
   * @param {Comparator} [customFindingComparator]
   * @return {MinHeap}
   */
  remove(item, customFindingComparator) {
    // Find number of items to remove.
    const customComparator = customFindingComparator || this.compare;
    const numberOfItemsToRemove = this.find(item, customComparator).length;

    for (let iteration = 0; iteration < numberOfItemsToRemove; iteration += 1) {
      // We need to find item index to remove each time after removal since
      // indices are being change after each heapify process.
      const indexToRemove = this.find(item, customComparator).pop();

      // If we need to remove last child in the heap then just remove it.
      // There is no need to heapify the heap afterwards.
      if (indexToRemove === (this.heapContainer.length - 1)) {
        this.heapContainer.pop();
      } else {
        // Move last element in heap to the vacant (removed) position.
        this.heapContainer[indexToRemove] = this.heapContainer.pop();

        // Get parent.
        const parentItem = this.hasParent(indexToRemove) ? this.parent(indexToRemove) : null;
        const leftChild = this.hasLeftChild(indexToRemove) ? this.leftChild(indexToRemove) : null;

        // If there is no parent or parent is less then node to delete then heapify down.
        // Otherwise heapify up.
        if (
          leftChild !== null
          && (
            parentItem === null
            || this.compare.lessThan(parentItem, this.heapContainer[indexToRemove])
          )
        ) {
          this.heapifyDown(indexToRemove);
        } else {
          this.heapifyUp(indexToRemove);
        }
      }
    }
    this.length -= 1;
    return this;
  }

  /**
   * @param {*} item
   * @param {Comparator} [customComparator]
   * @return {Number[]}
   */
  find(item, customComparator) {
    const foundItemIndices = [];
    const comparator = customComparator || this.compare;

    for (let itemIndex = 0; itemIndex < this.length; itemIndex += 1) {
      if (comparator.equal(item, this.heapContainer[itemIndex])) {
        foundItemIndices.push(itemIndex);
      }
    }

    return foundItemIndices;
  }

  /**
   * @param {number} [customStartIndex]
   */
  heapifyUp(customStartIndex) {
    // Take last element (last in array or the bottom left in a tree) in
    // a heap container and lift him up until we find the parent element
    // that is less then the current new one.
    let currentIndex = customStartIndex || this.heapContainer.length - 1;

    while (
      this.hasParent(currentIndex)
      && this.compare.lessThan(this.heapContainer[currentIndex], this.parent(currentIndex))
    ) {
      this.swap(currentIndex, this.getParentIndex(currentIndex));
      currentIndex = this.getParentIndex(currentIndex);
    }
  }

  /**
   * @param {number} [customStartIndex]
   */
  heapifyDown(customStartIndex) {
    // Compare the root element to its children and swap root with the smallest
    // of children. Do the same for next children after swap.
    let currentIndex = customStartIndex || 0;
    let nextIndex = null;

    while (this.hasLeftChild(currentIndex)) {
      if (
        this.hasRightChild(currentIndex)
        && this.compare.lessThan(this.rightChild(currentIndex), this.leftChild(currentIndex))
      ) {
        nextIndex = this.getRightChildIndex(currentIndex);
      } else {
        nextIndex = this.getLeftChildIndex(currentIndex);
      }

      if (this.compare.lessThan(this.heapContainer[currentIndex], this.heapContainer[nextIndex])) {
        break;
      }

      this.swap(currentIndex, nextIndex);
      currentIndex = nextIndex;
    }
  }

  /**
   * @return {boolean}
   */
  isEmpty() {
    return !this.heapContainer.length;
  }

  /**
   * @return {string}
   */
  toString() {
    return this.heapContainer.toString();
  }
}

// definition for a heap node
class Node {
    constructor(value, listNum, idx) {
      this.value = value;
      this.listNum = listNum;
      this.idx = idx;
    }

    getValue() {
        return this.value;
    }

    getListNum() {
        return this.listNum;
    }

    getIndex() {
        return this.idx;
    }

    setIndex(idx) {
        this.idx = idx;
    }

    setValue(value) {
        this.value = value;
    }
};

// Function to merge M sorted lists of variable length and
// print them in ascending order
printSorted(list) {
    // create an empty min-heap
    let comparator = new Comparator();
    let pq = new MinHeap(comparator);

    // push first element of each list into the min-heap
    // along with list number and their index in the list
    for (let i = 0; i < list.length; i++) {
        if (list[i].length > 0) {
            pq.add(new Node(list[i][0], i, 0));
        }
    }

    // run till min-heap is not empty
    let result = []       
    while (pq.length > 0) {
        // extract minimum node from the min-heap
        let min = pq.poll();
       // print the minimum element
        result.push(min.getValue());

        // take next element from "same" list and insert it into the
        // min-heap
        if (min.getIndex() + 1 < list[min.getListNum()].length) {
            min.setIndex(min.getIndex() + 1);
            min.setValue(list[min.getListNum()][min.getIndex()]);
            pq.add(min);
        }
    }
    return result;
}   

let list = [
        [10, 20, 30, 40],
        [15, 25, 35],
        [27, 29, 37, 48, 93],
        [32, 33]
      ]

printSorted(list); // => [ 10, 15, 20, 25, 27, 29, 30, 32, 33, 35, 37, 40, 48, 93 ]
```
