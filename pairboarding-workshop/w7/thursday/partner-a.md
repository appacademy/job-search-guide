# Partner A

## Behavioral
* What three things are you working on to improve your overall effectiveness?

## JS Trivia
* In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

```JavaScript
(function() {
    console.log(1);
    setTimeout(function(){console.log(2)}, 1000);
    setTimeout(function(){console.log(3)}, 0);
    console.log(4);
})();
```

## Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### Answer
The solution here is to keep track of the carry using a variable and simulate digits-by-digits sum starting from the head of list, which contains the least-significant digit.  Just like how you would sum two numbers on a piece of paper, we begin by summing the least-significant digits, which is the head of `l1` and `l2`. Since each digit is in the range of `0...9`, summing two digits may "overflow". For example 5 + 7 = 12. In this case, we set the current digit to 2 and bring over the `carry` = 1 to the next iteration. `carry` must be either 0 or 1 because the largest possible sum of two digits (including the `carry`) is 9 + 9 + 1 = 19. The time complexity of this algorithm is O(max(m,n)). Assume that m and n represents the length of `l1` and `l2` respectively, the algorithm above iterates at most max(m,n) times.  The space complexity is O(max(m,n)). The length of the new list is at most max(m,n)+1.

```JavaScript
const addTwoNumbers = (l1, l2) => {
    let dummyHead = new ListNode(0);
    let p = l1;
    let q = l2;
    let curr = dummyHead;
    let carry = 0;
    while (p != null || q != null) {
        let x = (p !== null) ? p.val : 0;
        let y = (q !== null) ? q.val : 0;
        let sum = carry + x + y;
        carry = Math.floor(sum / 10);
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (p !== null) p = p.next;
        if (q !== null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```
