# Partner B

## Good Enough?
* Tell me about a time you wouldn’t compromise on achieving a great outcome when others felt something was good enough.
* What was the situation?

## True Lies
* Since `[]` is a truthy value, will `[] == true` also return true?

### Answer
You are right about first part, `[]`, empty array is an object and objects are always truthy. Hence, if you use `if([]){console.log('its true')}` you will see the log.

However, there's a special case regarding `==` (double equal) in that it will do some implicit coercion.

Since the left and right side of the equality equation are of two different types, JavaScript can't compare them directly . So, under the hood, JavaScript will convert them to compare. First the right side of the equality will be coerced to a number; and `true` converted to a number is `1`.

After that, JavaScript will try to convert `[]` by using `toPrimitive` (from the JavaScript implementation). since `[].valueOf` is not primitive, it will use `toString` and will get `""`.

Now you are comparing `"" == 1` but the left and right is still not the same type. Therefore, the left side will be converted again to a number which in the case of the empty string will be `0`.

Finally, now that they're the same type, you are comparing `0 === 1` which will be false.

## Find the first k non-repeating characters in a string
* Given a string, find the first K non-repeating characters in it by doing only a single traversal of it.

```JavaScript
let str = "ABCDBAGHCHFAC";
let k = 3;
firstKNonRepeating(str, k); // => D G F
```

### Answer
A simple solution would be to store a count of each character in a map or an array by traversing it once.  Then we traverse the string once more to find the first K characters with a count of 1.  This has an O(n) time & space complexity but it violates our program constraints because we traverse the string twice.

We can solve this problem in a single traversal of the string.  The idea is to use a map to store each distinct character count and the index of its first or last occurrence in the string.  Then we traverse the map & push the index of all characters with a count of 1 into the max-heap.  Finally we pop K keys from the max-heap and that will be our first K non-repeating characters in the string.

Note that in this solution we are doing on complete traversal of the string and the map.  Since the size of the map is equal to the size of the alphabet (in a worst case scenario) it can safely be ignored because it takes up a constant amount of space.  Our heap size can be kept to O(K) by only pushing the first K characters into the max-heap & then for all subsequent elements in the map, if the current element is less than the root of the heap, we replace the root with it.  After we've processed every key in the map, the heap will contain the first K non-repeating characters.  The time complexity of this algorithm is O(Nlog(N)) and it takes O(K) space as mentioned above.

```JavaScript
// helper class for comparing two nodes
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

// definition of a Heap
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

// helper class for keeping track of a character's count and index
class Pair {
    constructor(count, index) {
        this.count = count;
        this.index = index;
    }

    getCount() {
        return this.count;
    }

    getIndex() {
        return this.index;
    }

    setCount(count) {
        this.count = count;
    }

    setIndex(index) {
        this.index = index;
    }
}

// Function to find the first k non-repeating character in
// the string by doing only one traversal of it
const firstKNonRepeating = (str, k) => {
    // map to store character count and the index of its
    // last occurrence in the string
    let map = {};

    for (let i = 0 ; i < str.length; i++)
    {
        if (map[str.charAt(i)] === undefined) {
            map[str.charAt(i)] = new Pair(1, i);
        }
        else {
            let pair = map[str.charAt(i)];
            pair.setCount(pair.getCount() + 1);
            pair.setIndex(i);
        }
    }

    // create an empty max-heap (max size k)
    let comparator = new Comparator;
    let pq = new MinHeap(comparator.reverse());

    // traverse the map and process index of all characters
    // having count of 1
    for (let key in map) {
        let count = map[key].getCount();
        let index = map[key].getIndex();

        if (count == 1) {
            // if heap has less than k keys in it
            // push index of current character
            if (--k >= 0) {
                pq.add(index);
            }
            // else if index of current element is less than the root
            // of the heap, replace the root with the current element
            else if (index < pq.peek()) {
                pq.poll();
                pq.add(index);
            }
        }
    }

    // Now the heap contains index of count k non-repeating characters

    // pop all keys from the max-heap
    while (pq.length > 0) {
        // extract the maximum node from the max-heap
        let max_index = pq.poll();
        console.log(str.charAt(max_index) + " ");
    }
}


let str = "ABCDBAGHCHFAC";
let k = 3;

firstKNonRepeating(str, k); // => D G F
```
