# Partner A

## Linking Problems
* Tell me about a time when you linked two or more problems together and identified an underlying issue?
* Were you able to find a solution?

## Function Blocks
* What is the significance of, and reason for, wrapping the entire content of a JavaScript source file in a function block?

### Answer
This is an increasingly common practice, employed by many popular JavaScript libraries (jQuery, Node.js, etc.). This technique creates a closure around the entire contents of the file which, perhaps most importantly, creates a private namespace and thereby helps avoid potential name clashes between different JavaScript modules and libraries.

Another feature of this technique is to allow for an easily referenceable (presumably shorter) alias for a global variable. This is often used, for example, in jQuery plugins. jQuery allows you to disable the $ reference to the jQuery namespace, using `jQuery.noConflict()`. If this has been done, your code can still use $ employing this closure technique, as follows:

`(function($) { /* jQuery plugin code referencing $ */ } )(jQuery);`

## Kth Smallest Element in a BST
* Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Example 1:
```
Input: root = [3,1,4,null,2], k = 1

   3
  / \
 1   4
  \
   2

Output: 1
```

Example 2:
```
Input: root = [5,3,6,2,4,null,null,1], k = 3

       5
      / \
     3   6
    / \
   2   4
  /
 1

Output: 3
```
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?


### Answer
We can solve this problem efficiently by keeping track of the number of nodes in the left subtree.  If the number of nodes in the left subtree is equal to `k - 1` we can simply return the root.  If the number of nodes in the left subtree is `> k - 1` we recursively call `kthSmallest` on `root.left`.  If the number of nodes in the left subtree is `< k - 1` we recursively call `kthSmallest` on `root.right` and we subtract the number of nodes we've seen so far from `k`.

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
 * @param {number} k
 * @return {number}
 */
const kthSmallest = function(root, k) {
    let left = nodeCount(root.left);
    if (left + 1 === k) {
        return root.val;
    } else if (left + 1 < k) {
        return kthSmallest(root.right, k - left - 1);
    } else {
        return kthSmallest(root.left, k);
    }
};

const nodeCount = (root) => {
    if (root === null) {
        return 0;
    }
    return 1 + nodeCount(root.left) + nodeCount(root.right);
}
```
The idea behind the follow up question is to determine what extra information is required for the divide-and-conquer strategy. Basically because we can know the number of nodes on the left subtree, we get to know what the position of the root node is, in the in-order traversal, which is basically the the kth number. The left value can be saved in each node of the tree, and when we are finding the kth number. The time complexity of the above solution is O(n) because we have to traverse half the tree (n/2) before you get the right answer and 2 is a constant.
