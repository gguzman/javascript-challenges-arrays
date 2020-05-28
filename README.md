# Javascript challenges

### Problem 1:
```
Given an array a that contains only numbers in the range
from 1 to a.length, find the first duplicate number for
which the second occurrence has the minimal index. In other words, if
there are more than 1 duplicated numbers, return the number for
which the second occurrence has a smaller index than the second
occurrence of the other number does. If there are no such elements,
return -1.
```

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
