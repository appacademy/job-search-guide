# Partner B

## A matter of policy
* Give me a specific example of a time when you had to conform to a policy with which you did not agree with

## Purely Functional
* What is a pure function?

### Answer
A pure function is a function that doesn't depend on and doesn't modify the states of variables out of its scope. Essentially, this means that a pure function will always return the same result given same parameters.

## Delete a node in a BST
* Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

Note: Time complexity should be O(height of tree).

Example:

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

### Answer
Our rules for deleting a node from a BST are as follows:
1. If a node has no children, simply remove it.
2. If a node has only one child, delete it and promote its child to take its place.
3. If a node has two children, find the largest node in its left subtree and promote that node to replace the deleted node. If necessary, promote that node's child to replace its parent.

```JavaScript
/**
* Definition for a binary tree node.
* function TreeNode(val) {
*     this.val = val;
*     this.left = this.right = null;
* }
*/
/**
* @param {TreeNode} root
* @param {number} key
* @return {TreeNode}
*/

// helper function to find the node
const findNode = (root, key) => {
  if (root === null) return null;
  if (root.val === key) return root;
  if (root.val < key) return findNode(root.right, key);
  if (root.val > key) return findNode(root.left, key);
}

// helper function to find the parent of a node
const findParent = (root, key) => {
  if (root === null || root === undefined) return null;
  if (root.left !== null && root.left.val === key) return root;
  if (root.right !== null && root.right.val === key) return root;
  if (root.val > key) {
      return findParent(root.left, key);
  } else {
      return findParent(root.right, key);
  }
}

// helper function to delete the child node given a parent
const deleteChildFromParent = (parent, child) => {
  return parent.left && parent.left.val === child.val ?
  parent.left = null : parent.right = null;
}

const promoteGrandChild = (parent, child) => {
  let grandChild = child.right === null ? child.left : child.right;
  if (parent === null) return grandChild;
  parent.left !== null && parent.left.val === child.val ? parent.left = grandChild : parent.right = grandChild;
}

const promoteMaxNode = (currNode, maxNode, parentOfMax, childOfMax) => {
  currNode.val = maxNode.val;
  console.log(parentOfMax)
  parentOfMax.right = childOfMax;
}

const maximum = (root) => {
  if (root === null) return null;
  if (root.right === null) return root;
  return maximum(root.right);
}

const deleteNode = function(root, key) {
  let parentNode = findParent(root, key);
  let currNode = findNode(root, key);
  if (currNode == null) return root;
  // if the node has no children
  if (currNode.left === null && currNode.right === null) {
      if (parentNode === null) {
          root = null;
          return root;
      }
      deleteChildFromParent(parentNode, currNode);

      // if the node has 1 child
  } else if (currNode.left !== null && currNode.right === null ||
            currNode.left === null && currNode.right !== null) {
      let grandChild = promoteGrandChild(parentNode, currNode);
      return grandChild === undefined ? root : grandChild;

      // if the node has two children
  } else {
      let maxNode = maximum(root.left) || maximum(root);
      let parentOfMax = findParent(root, maxNode.val)
      let childOfMax = maxNode.left;
      promoteMaxNode(currNode, maxNode, parentOfMax, childOfMax);
      return root;
  }
  return root;

};
```
