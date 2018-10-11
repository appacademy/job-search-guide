## Behavioral Questions

* Tell me about yourself by walking me through your resume.
* What was your biggest failure? The answer should tell the interviewer the following:
  * What was the context for the situation that led to the failure?
  * What lead up to the failure?
  * What, specifically, was the failure?
  * How did you recover from this failure? What was the eventual outcome?

## Trivia

* [What is the event loop?](https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40)
* [What are some of your favorite features of ES6?](https://webapplog.com/es6/)

## `merge_sort`

Implement merge sort.

### Solution

```ruby
def merge_sort(array)
  # already sorted
  return array if array.count < 2

  middle = array.count / 2
  left, right = array.take(middle), array.drop(middle)

  sorted_left, sorted_right = merge_sort(left), merge_sort(right)

  merge(sorted_left, sorted_right)
end

def merge(left, right)
  merged_array = []
  until left.empty? || right.empty?
    merged_array <<
      ((left.first < right.first) ? (left.shift) : (right.shift))
  end

  merged_array + left + right
end
```

Time complexity: `O(n*log(n))`.

```ruby
def merge(left, right)
  merged_array = []
  i, j = 0, 0
  until i == left.length || j == right.length
    if left[i] > right[j]
      merged_array << right[j]
      j += 1
    else
      merged_array << left[i]
        i += 1
    end
  end
  merged_array + left.drop(i) + right.drop(j)
end
```

Time complexity for merge only: `O(n)`.

## Matchsticks

You have two sticks and a matchbox. Each stick takes exactly an hour
to burn from one end to the other.

The sticks are weird, in that they do not burn at a steady. If you
break a stick in half, it is not guaranteed that each half will take
30min to burn.

How would you measure exactly 45 minutes by burning these sticks?

### Solution

Take stick1, light it at both ends. At the same time, light stick2 at
one end.

When stick1 is extinguished, 30min have passed. Now, light stick2 at
the other end. The stick will take another 15min to finish burning.

# Largest Difference

Given an array of integers, find the largest difference between two elements such that the element of lesser value must come before the greater element. **Complete this problem in `O(n)` time**.

**Examples:**

```js
findLargestDifference([1, 6, 5, 2, 9, -2])

// Output is 8 based on the difference between 1 and 9. Note: It is not 11 from 9 and -2 because 9 comes before -2.
```

## Solution

```javascript
function findLargestDifference(array) {
  // If there is only one element, there is no difference
  if (array.length <= 1) return -1;

  // currentMin will keep track of the current lowest
  let currentMin = array[0];
  let currentMaxDifference = 0;

  // We will iterate through the array and keep track of the current max difference
  // If we find a greater max difference, we will set the current max difference to that variable
  // Keep track of the current min as we iterate through the array, since we know the greatest
  // difference is yield from `largest value in future` - `smallest value before it`

  for (let i = 1; i < array.length; i++) {
    if (array[i] > currentMin && (array[i] - currentMin > currentMaxDifference)) {
      currentMaxDifference = array[i] - currentMin;
    } else if (array[i] <= currentMin) {
      currentMin = array[i];
    }
  }

  // If negative or 0, there is no largest difference
  if (currentMaxDifference <= 0) return -1;

  return currentMaxDifference;
}
```
