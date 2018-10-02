# Partner B

## Behavioral
* Tell me about a time when you realized you needed to have a deeper level of subject matter expertise to do your job well?

## Arguments and Call
* Write a simple function in JavaScript to tell whether `2` is a passed parameter or not.

### Answer
`arguments` is a local variable, available inside all functions that provides a collection of all the arguments passed to the function. `arguments` is not an array rather an array like object. It has length but doesn't have the methods like `forEach`, `indexOf`, etc.  First we convert `arguments` to an array by calling the `slice` method on it. After that simply use `indexOf`.

```JavaScript
function isTwoPassed(){
  var args = Array.prototype.slice.call(arguments);
  return args.indexOf(2) != -1;
}

isTwoPassed(1,4) //false
isTowPassed(5,3,1,2) //true
```

## Flatten Binary Tree to Linked list
* Given a binary tree, flatten it to a linked list in-place.

For Example, given the following tree:

```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

### Answer
We can solve this question with a simple DFS technique.  See solution below:

```JavaScript
const flatten = function(root) {
    let stack = [root];
    let last = new TreeNode(null);
    while (stack.length > 0) {
        let node = stack.pop();
        last.right = node;
        last.left = null;
        if (node && node.right !== null); stack.push(node.right);
        if (node && node.left !== null); stack.push(node.left);
        last = node;
    }
};
```
