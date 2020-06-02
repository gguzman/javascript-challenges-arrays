# Javascript challenges

## Problem 1.- First Duplicate in Array:

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
const firstDuplicate = a => {
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
>You can choose to solve this problem without obeying the O(1) memory constraint. Once you have solved it, you will be able to look at other people's solutions!

>If you do want to solve it within the memory limit, the restrictions on the values a[i] are critical in this problem. Changing the array in place doesn't require extra memory.

#### Solution 2.- The memory approach
```
const firstDuplicateWithMemory = arr => {
    let memory = {};

    for(let i = 0; i < arr.length; i++) {
        let item = arr[i];
        if(memory[item] !== undefined)
            return item;
        else
            memory[item] = i;
    }

    return -1;
};
```
>This time, we need to iterate the array only once. The complexity to iterate the array once will be O(N). Storing and retrieving an item from an object has a complexity of O(1), so our final time complexity will be O(N). But, in this case, we are introducing an O(N) space complexity too since we are storing the elements of the array once again.


## Problem 2.- First Not Repeating Character:

>Given a string `s` consisting of small English letters, find and return the first instance of a non-repeating character in it. If there is no such character, return `'_'`.

### Example

For `s = "abacabad"`, the output should be
`firstNotRepeatingCharacter(s) = 'c'`.

There are 2 non-repeating characters in the string: `'c'` and `'d'`. Return `c` since it appears in the string first.

For `s = "abacabaabacaba"`, the output should be
`firstNotRepeatingCharacter(s) = '_'`.

There are no characters in this string that do not repeat.

### Input/Output

**[execution time limit] 4 seconds (js)**

**[input] string s**

A string that contains only lowercase English letters.

Guaranteed constraints:
`1 ≤ s.length ≤ 105.`

**[output] char**

The first non-repeating character in `s`, or `'_'` if there are no characters that do not repeat.

### Solution

```
function firstNotRepeatingCharacter(s) {

    for(let i=0;i<s.length;i++) {
        if (s.length === 1) return s[i]
        if (s.indexOf(s[i], s.indexOf(s[i]) + 1) === -1) return s[i]
    }
    return '_';
}
```

## Problem 3.- First Unique Character in a String:

>Given a string `s`, find the first non-repeating character in it and return it's index. If it doesn't exist, return `-1`.

### Example

```
s = "leetcode"
return 0
```
```
s = "loveleetcode",
return 2
```
```
s = "abcdfabcdf",
return -1
```
Note: You may assume the string contains only lowercase letters.

### Solution

```
function firstUniqueCharacter(s) {
    for(let i=0;i<s.length;i++) {
        if (s.length === 1) return i;
        if (s.indexOf(s[i], s.indexOf(s[i]) + 1) === -1) return i;
    }
    return -1;
}
```

## Problem 4.- Rotate image:

>Note: Try to solve this task in-place (with O(1) additional memory), since this is what you'll be asked to do during an interview.

>You are given an n x n 2D matrix that represents an image. Rotate the image by 90 degrees (clockwise).

### Example
For
```
a = [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]]
```
the output should be
```
rotateImage(a) =
    [[7, 4, 1],
     [8, 5, 2],
     [9, 6, 3]]
```

### Solution with ES6
```
function rotateImage(arr) {
    const N = matrix.length - 1;   // use a constant
    
    // use arrow functions and nested map;
    const result = matrix.map((row, i) => 
         row.map((val, j) => matrix[N - j][i])
    );
    
    matrix.length = 0;       // hold original array reference
    matrix.push(...result);  // Spread operator

    return matrix;
}

```

### Solution.- If the performance is important

If performance is important, as mentioned above, it would be good to use for.
```
function rotateMatrix() {    
    const n = this.m[0].length;

    let res = []

    for (let i = 0; i < n; ++i) {
      for (let j = 0; j < n; ++j) {
         if (!res[j])
           res[j] = []
         res[j][i] = this.m[n-1-i][j];
      }
    }
    return res;
}
```

## Problem 5.- Sudoku2

>Sudoku is a number-placement puzzle. The objective is to fill a `9 × 9` grid with numbers in such a way that each column, each row, and each of the nine `3 × 3` sub-grids that compose the grid all contain all of the numbers from `1` to `9` one time.

>Implement an algorithm that will check whether the given `grid` of numbers represents a valid Sudoku puzzle according to the layout rules described above. Note that the puzzle represented by `grid` does not have to be solvable.

### Example
For
```
grid = [['.', '.', '.', '1', '4', '.', '.', '2', '.'],
        ['.', '.', '6', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '1', '.', '.', '.', '.', '.', '.'],
        ['.', '6', '7', '.', '.', '.', '.', '.', '9'],
        ['.', '.', '.', '.', '.', '.', '8', '1', '.'],
        ['.', '3', '.', '.', '.', '.', '.', '.', '6'],
        ['.', '.', '.', '.', '.', '7', '.', '.', '.'],
        ['.', '.', '.', '5', '.', '.', '.', '7', '.']]
```

the output should be
`sudoku2(grid) = true;`

For
```
grid = [['.', '.', '.', '.', '2', '.', '.', '9', '.'],
        ['.', '.', '.', '.', '6', '.', '.', '.', '.'],
        ['7', '1', '.', '.', '7', '5', '.', '.', '.'],
        ['.', '7', '.', '.', '.', '.', '.', '.', '.'],
        ['.', '.', '.', '.', '8', '3', '.', '.', '.'],
        ['.', '.', '8', '.', '.', '7', '.', '6', '.'],
        ['.', '.', '.', '.', '.', '2', '.', '.', '.'],
        ['.', '1', '.', '2', '.', '.', '.', '.', '.'],
        ['.', '2', '.', '.', '3', '.', '.', '.', '.']]
```
the output should be
`sudoku2(grid) = false.`
>The given grid is not correct because there are two 1s in the second column. Each column, each row, and each 3 × 3 subgrid can only contain the numbers 1 through 9 one time.

**Input/Output**

**[execution time limit]** 4 seconds (js)

**[input]** array.array.char grid

A `9 × 9` array of characters, in which each character is either a digit from '1' to '9' or a period '.'.

**[output]** boolean

Return `true` if `grid` represents a valid Sudoku puzzle, otherwise return `false`.

### Solution
```
function sudoku2(grid) {
  return rowIsValid(grid) && columnIsValid(grid) && squareIsValid(grid)
}

let rowIsValid = (grid) => {
  let result = true;
  for (let i = 0; i < grid.length; i++) {
    let set = new Set();
    for (let j = 0; j < grid[i].length; j++) {
      let cell = grid[j][i];
      if (cell !== '.') {
        if (set.has(cell)) {
          result = false;
          break;
        } else {
          set.add(cell);
        }
      }
    }
  }
  return result;
}

let singleRowIsValid = (row) => {
  
}

let columnIsValid = (grid) => {
  for (let i = 0; i < grid.length; i++) {
    let column = grid[i]
    if ( !singleColumnIsValid(column) ) {
      console.log('line 12')
      return false;
    };
  }
  return true;
}

let singleColumnIsValid = (column) => {
  let set = new Set();
  for (let i = 0; i < column.length; i++) {
    let cell = column[i]
    if ( cell !== '.') {
      if ( set.has(cell) ) {
        console.log('line 23', 'set', set, 'cell', cell)
        return false
      } else {
        set.add(cell)
      }
    }
  }
  return true;
}

let squareIsValid = (grid) => {
  let result = true;
  for (let i = 0; i < grid.length; i+=3) {
    for (let j = 0; j < grid[i].length; j+=3) {
      let square = [];
      square.push(grid[i][j]);
      square.push(grid[i][j+1]);
      square.push(grid[i][j+2]);
      square.push(grid[i+1][j]);
      square.push(grid[i+1][j+1]);
      square.push(grid[i+1][j+2]);
      square.push(grid[i+2][j]);
      square.push(grid[i+2][j+1]);
      square.push(grid[i+2][j+2]);
      console.log('square =>', square)
      let set = new Set();
      for (let k = 0; k < square.length; k++) {
        let cell = square[k];
        if ( cell !== '.') {
          if (set.has(cell)) {
            console.log('false')
            result = false;
            break;
          } else {
            set.add(cell)
          }
        }
      }
    }
  }

  return result;
};
```
