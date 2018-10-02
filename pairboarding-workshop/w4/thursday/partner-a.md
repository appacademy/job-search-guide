# Partner A

## Who likes you
* Tell me about a time you were able to successfully deal with another person even when that individual
may not have personally liked you (or vice versa).

## Trivia
* Consider the two functions below. Will they both return the same thing? Why or why not?

```JavaScript
function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}
```

### Answer
Not only is this surprising, but what makes this particularly gnarly is that `foo2()` returns undefined without any error being thrown.

The reason for this has to do with the fact that semicolons are technically optional in JavaScript (although omitting them is generally really bad form). As a result, when the line containing the `return` statement (with nothing else on the line) is encountered in `foo2()`, a semicolon is automatically inserted immediately after the return statement.

No error is thrown since the remainder of the code is perfectly valid, even though it doesn’t ever get invoked or do anything (it is simply an unused code block that defines a property `bar` which is equal to the string `"hello"`).

This behavior also argues for following the convention of placing an opening curly brace at the end of a line in JavaScript, rather than on the beginning of a new line. As shown here, this becomes more than just a stylistic preference in JavaScript.

## Find the in-order successor for a given key in a BST
* Given a BST, find the in-order successor of a given key in it.  If the given key doesn't appear in the BST, then return the next greater key (if any) present in the BST.

An in-order successor of a node in a BST is the next node in the in-order traversal of it.  Consider the below BST:

```
      15
    /    \
  10      20
 /  \     / \
8   12  16   25

- The in-order successor of 8 is 10
- The in-order successor of 12 is 15
- The in-order successor of 25 doesn't exist
```

### Answer
A node's in-order successor is the node with the least value in its right subtree (i.e. its right subtree's left-most child).  If the right subtree of the node doesn't exist, then the in-order successor is one of the ancestors of it.  To find which ancestor is the successor, we can move up the tree towards the root until we encounter a node which is the left child of its parent.  If any such node is found, the in-order successor is its parent.  Otherwise there is no in-order successor for the node.

To solve this problem we can recursively check the above conditions.  The idea is to search for a given node in the tree and update the successor to the current node before visiting its left subtree.  If the node is found in the BST, then we return the node with the least value in its right subtree and if the right subtree of the node doesn't exist, then the in-order successor is one of the ancestors of it which has already been updated while searching for the given key.

```JavaScript
// Data structure to store a Binary Search Tree node
class Node {
    constructor(data) {
        this.data = data;
        this.left = null;
        this.right = null;
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


    // Helper function to find minimum value node in given BST
    findMinimum(root) {
        while (root.left !== null) {
            root = root.left;
        }
        return root;
    }

    // Recursive function to find inorder successor for given key in a BST
    findSuccessor(root, succ, key) {
        // base case
        if (root === null) {
            return succ;
        }

        // if node with key's value is found, the successor is minimum value
        // node in its right subtree (if any)
        // console.log(key, parseInt(root.data))
        if (root.data === parseInt(key)) {
            if (root.right !== null) {
                return this.findMinimum(root.right);
            }
        }

        // if given key is less than the root node, recuse for left subtree
        else if (key < parseInt(root.data)) {
            // update successor to current node before recursing in left subtree
            succ = root;
            return this.findSuccessor(root.left, succ, key);
        }

        // if given key is more than the root node, recuse for right subtree
        else {
            return this.findSuccessor(root.right, succ, key);
        }

        return succ;
    }
}
// main function

let root = null;

/* Construct below tree
      15
      /  \
    /    \
    10     20
  / \     / \
  /   \   /   \
8    12 16   25
*/

let bst = new BST
let keys = [ 8, 10, 12, 15, 16, 20, 25 ];
for (let key in keys) {
    root = bst.insert(root, keys[key]);
}

// find inorder successor for each key
for (let key in keys) {
    console.log(keys[key] + " ");

    let succ = bst.findSuccessor(root, null, keys[key]);
    if (succ !== null) {
        console.log("Successor is " + succ.data);
    } else {
        console.log("No Successor");
    }
}

// => 8
// Successor is 10
// 10
// Successor is 12
// 12
// Successor is 15
// 15
// Successor is 16
// 16
// Successor is 20
// 20
// Successor is 25
// 25
// No Successor
```
