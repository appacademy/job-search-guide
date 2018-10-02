# Partner A

## Behavioral
* What are types of projects you like to work on?  
* Don’t like?  
* Why?

## Window & Document
* Is there any difference between window and document?

### Answer
Yes. JavaScript has a global object and everything runs under it. window is that global object that holds global variables, global functions, location, history everything is under it. Besides, setTimeout, ajax call (XMLHttpRequest), console or localStorage are part of window.

document is also under window. document is a property of the window object. document represents the DOM and DOM is the object oriented representation of the html markup you have written. All the nodes are part of document. Hence you can use getElementById or addEventListener on document. These methods are not present in the window object.

```JavaScript
window.document === document; //true
window.getElementById; //undefined
document.getElementById; //function getElementById() { [native code] }
```

## Counting Zeros
* Count Total number of zeros from `1` upto `n`?

### Answer

 If `n = 50`. number of `0`s would be `11` (`0`, `10`, `20`, `30`, `40`, `50`, `60`, `70`, `80`, `90`, `100`). Please note that 100 has two `0`s. This one looks simple but can be a little tricky.

```JavaScript
function countZero(n){
  var count = 0;
  while(n > 0){
   count += Math.floor(n / 10);
   n = n / 10;
  }
  return count;
}

> countZero(2014);
  = 223
```

So the tick here is if you have a `n = 50` then the range is `1` to `50` the number of zeros is `5`. Which is just `50` divided by `10`. However, if `n` is 100 then the number of zeros is `11`. You can can catch this edge case by taking `100/10` which is `10` and then you take that `10` and preform `10/10` which is `1`. You can then add those two together to get the correct answer. Thats how you catch the extra zeros when `n` is a number like (`100`, `200`, `1000`)


## Out of place numbers
You are given an almost sorted array of length k.  Write a function that will return the number of out of place elements that can be removed while leaving only the sorted array leftover.  Elements can only be taken out of the array one at a time and the leftover array must remain sorted each time you take an element out.  If taking an element out would cause the array to be unsorted than you may not remove that element.  If no elements can be removed than return `0`.

```ruby
def outOfPlaceChecker(arr)
    out_of_place = false
    i = 0

    while i < arr.length-1
      if arr[i] > arr[i+1] && out_of_place == true
        return nil
      end

      if arr[i] > arr[i+1]
        out_of_place = true

        if arr[i + 2] && arr[i + 2] > arr[i]
          out_of_place_value = 2
        else
          out_of_place_value = 1
        end
      end

      i+=1
    end

    if out_of_place
      return out_of_place_value
    end

    return arr.length
end

outOfPlaceChecker([2,1,3,4])
```
