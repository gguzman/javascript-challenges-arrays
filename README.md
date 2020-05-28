# Javascript challenges

### Problem.- First Duplicate in Array:

>Given an array a that contains only numbers in the range
>from 1 to a.length, find the first duplicate number for
>which the second occurrence has the minimal index. In other words, if
>there are more than 1 duplicated numbers, return the number for
>which the second occurrence has a smaller index than the second
>occurrence of the other number does. If there are no such elements,
>return -1.


#### Solution 1
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
>While this solution works, it has a time complexity of O(N2).
>Surely there must be a better solution...

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
>This time, we need to iterate the array only once. The complexity to iterate the array once will be O(N). Storing and >retrieving an item from an object has a complexity of O(1), so our final time complexity will be O(N). But, in this case, we >are introducing an O(N) space complexity too since we are storing the elements of the array once again.
