# Partner B

## Can you cope?
* Describe a time when you were faced with a stressful situation that demonstrated your coping skills.

## Is Integer?
* Discuss possible ways to write a function isInteger(x) that determines if x is an integer.

### Answer
This may sound trivial and, in fact, it is trivial with ECMAscript 6 which introduces a new `Number.isInteger()` function for precisely this purpose. However, prior to ECMAScript 6, this is a bit more complicated, since no equivalent of the `Number.isInteger()` method is provided.

The issue is that, in the ECMAScript specification, integers only exist conceptually; i.e., numeric values are always stored as floating point values.

With that in mind, the simplest and cleanest pre-ECMAScript-6 solution (which is also sufficiently robust to return false even if a non-numeric value such as a string or null is passed to the function) would be the following use of the bitwise XOR operator:

`function isInteger(x) { return (x ^ 0) === x; }`

The following solution would also work, although not as elegant as the one above:

`function isInteger(x) { return Math.round(x) === x; }`

Note that `Math.ceil()` or `Math.floor()` could be used equally well (instead of Math.round()) in the above implementation.

Or alternatively:

`function isInteger(x) { return (typeof x === 'number') && (x % 1 === 0); }`

One fairly common incorrect solution is the following:

`function isInteger(x) { return parseInt(x, 10) === x; }`

While this `parseInt`-based approach will work well for many values of `x`, once `x` becomes quite large, it will fail to work properly. The problem is that `parseInt()` coerces its first parameter to a string before parsing digits. Therefore, once the number becomes sufficiently large, its string representation will be presented in exponential form (e.g., `1e+21`). Accordingly, parseInt() will then try to parse `1e+21`, but will stop parsing when it reaches the `e` character and will therefore return a value of `1`. Observe:

```
> String(1000000000000000000000)
'1e+21'
> parseInt(1000000000000000000000, 10)
1
> parseInt(1000000000000000000000, 10) === 1000000000000000000000
false
```

## Determine if a given Binary Tree is a BST or not
* Given the root node of a binary tree.  Determine if it represents a BST or not.

### Answer
This problem has a simple recursive solution. The BST property "every node in the right subtree has to be larger than the current node and every node on the left subtree has to be smaller than the current node" is the key to figuring out whether a tree is a BST or not.

The greedy algorithm - simply traverse the tree, at every node check whether the node contains a value larger than the value at the left child & smaller than the the value on the right child - does not work for all cases.  Consider the following tree:

```
  20
 /  \
10  30
    / \
   5   40
```
In the tree above, each node meets the condition that the node contains a value larger than its left child and smaller than its right child, but it is still not a BST.  The value 5 is in the right subtree of the node containing 20 (a violation of the BST property).

Instead of making a decision based solely on the values of a node and its children, we also need information flowing down from the parent as well.  In the tree above, if we could remember the node containing 20, we would see that the node with a value of 5 is violating the BST property.  Therefore the condition we need to check at each node is:

* If the node is a left child of its parent, then it must be smaller than (or equal to) the parent and it must pass down the value from its parent to its right subtree to make sure none of the nodes in that subtree are greater than the parent

* If the node is a right child of its parent, then it must be larger than the parent and it must pass down the value from its parent to left subtree to make sure none of the nodes in that subtree are less than the parent.


```JavaScript
// Data structure to store a Binary Search Tree node
class Node {
    constructor(data) {
        this.data = data;
        this.left;
        this.right;
    }
}

class BST {
    // Recursive function to insert an key into BST
    insert(root, key) {
        // if the root is null, create a new node an return it
        if (root == null) {
            return new Node(key);
        }

        // if given key is less than the root node, recurse for left subtree
        if (key < root.data) {
            root.left = this.insert(root.left, key);
        }
        // if given key is more than the root node, recurse for right subtree
        else {
            root.right = this.insert(root.right, key);
        }

        return root;
    }

    // Function to determine if given Binary Tree is a BST or not by keeping a
    // valid range (starting from [MIN_VALUE, MAX_VALUE]) and keep shrinking
    // it down for each node as we go down recursively
    isBST(node, minKey, maxKey) {
        // base case
        if (node == null) {
            return true;
        }

        // if node's value fall outside valid range
        if (node.data < minKey || node.data > maxKey) {
            return false;
        }

        // recursively check left and right subtrees with updated range
        return this.isBST(node.left, minKey, node.data) &&
            this.isBST(node.right, node.data, maxKey);
    }

    // Function to determine if given Binary Tree is a BST or not
    determineBST(root) {
        if (this.isBST(root, -Infinity, Infinity)) {
            console.log("This is a BST.");
        } else {
            console.log("This is NOT a BST!");
        }
    }

    swap(root) {
        let left = root.left;
        root.left = root.right;
        root.right = left;
    }
}

// set up tree for test
let root = null;
let keys = [ 15, 10, 20, 8, 12, 16, 25 ];
let bst = new BST();

for (let key in keys) {
    root = bst.insert(root, keys[key]);
}

// swap left and right nodes to make tree invalid
bst.swap(root);

bst.determineBST(root); // => This is NOT a BST.
```

The time & space complexity of the above solution are both O(n)
