# Javascript challenges

### Problem.- First Duplicate in Array:

>Given an array a that contains only numbers in the range
from 1 to a.length, find the first duplicate number for
which the second occurrence has the minimal index. In other words, if
there are more than 1 duplicated numbers, return the number for
which the second occurrence has a smaller index than the second
occurrence of the other number does. If there are no such elements,
return -1.

### Example

For `a = [2, 1, 3, 5, 3, 2]`, the output should be `firstDuplicate(a) = 3`.

There are 2 duplicates: numbers 2 and 3. The second occurrence of 3 has a smaller index than the second occurrence of 2 does, so the answer is 3.

For `a = [2, 2]`, the output should be `firstDuplicate(a) = 2`;

For `a = [2, 4, 3, 5, 1]`, the output should be `firstDuplicate(a) = -1`.

### Input/Output

**[execution time limit]** 4 seconds (js)

**[input]** array.integer a

Guaranteed constraints:
`1 ≤ a.length ≤ 105,`
`1 ≤ a[i] ≤ a.length.`

**[output]** integer

The element in a that occurs in the array more than once and has the minimal index for its second occurrence. If there are no such elements, return -1.


#### Solution 1
```
const firstDuplicate = arr => {
    let smaller = 1000000;
    let duplicates = [];

    for(let i=0;i<a.length;i++) {
        let item = a[i];
        if (!duplicates.includes(item)) {
            let secondItemIndex = a.indexOf(item, a.indexOf(item) + 1)
            if ( secondItemIndex != -1) {
                duplicates.push(item)
                if (secondItemIndex < smaller) {
                    smaller = secondItemIndex;
                }
            }
        }
    }

    if (duplicates.length > 0) {
        return a[smaller];
    } else {
        return -1;
    }
};
```
>While this solution works, it has a time complexity of O(N2).Surely there must be a better solution...

#### Solution 2
```
const firstDuplicateWithMemory = arr => {
  const memory = {};

  for (let i = 0; i < arr.length; i++) {
    if (memory[arr[i]] !== undefined) {
      return arr[i];
    } else {
      memory[arr[i]] = arr[i];
    }
  }

  return -1;
};
```
>This time, we need to iterate the array only once. The complexity to iterate the array once will be O(N). Storing and retrieving an item from an object has a complexity of O(1), so our final time complexity will be O(N). But, in this case, we are introducing an O(N) space complexity too since we are storing the elements of the array once again.
