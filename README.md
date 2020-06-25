# Javascript challenges - Arrays
## Content
- [Problem 1.- First Duplicate in Array](/README.md#problem-1--first-duplicate-in-array)
- [Problem 2.- First Not Repeating Character](/README.md#problem-2--first-not-repeating-character)
- [Problem 3.- First Unique Character in a String](/README.md#problem-3--first-unique-character-in-a-string)
- [Problem 4.- Rotate image](/README.md#problem-4--rotate-image)
- [Problem 5.- Sudoku2](/README.md#problem-5--sudoku2)
- [Problem 6.- Is Crypt solution](/README.md#problem-6--is-crypt-solution)
- [Problem 7.- Is Beautiful string](/README.md#problem---is-beautiful-string)


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


### Solution 1
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

### Solution 2.- The memory approach
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
>El método **indexOf()** retorna el primer índice en el que se puede encontrar un elemento dado en el array, ó retorna `-1` si el elemento no esta presente.

>Sintaxis.- `array.indexOf(searchElement[, fromIndex])`

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

### Input/Output

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

## Problem 6.- Is Crypt Solution

>A _cryptarithm_ is a mathematical puzzle for which the goal is to find the correspondence between letters and digits, such that the given arithmetic equation consisting of letters holds true when the letters are converted to digits.

>You have an array of strings `crypt`, the cryptarithm, and an an array containing the mapping of letters and digits, `solution`. The array `crypt` will contain three non-empty strings that follow the structure: `[word1, word2, word3]`, which should be interpreted as the `word1 + word2 = word3` cryptarithm.

>If `crypt`, when it is decoded by replacing all of the letters in the cryptarithm with digits using the mapping in `solution`, becomes a valid arithmetic equation containing no numbers with leading zeroes, the answer is `true`. If it does not become a valid arithmetic solution, the answer is `false`.

>**Note** that number `0` doesn't contain leading zeroes (while for example `00` or `0123` do).

### Example
For `crypt = ["SEND", "MORE", "MONEY"]` and
```
solution = [['O', '0'],
            ['M', '1'],
            ['Y', '2'],
            ['E', '5'],
            ['N', '6'],
            ['D', '7'],
            ['R', '8'],
            ['S', '9']]
```
the output should be
`isCryptSolution(crypt, solution) = true`.

When you decrypt `"SEND"`, `"MORE"`, and `"MONEY"` using the mapping given in `crypt`, you get `9567 + 1085 = 10652` which is correct and a valid arithmetic equation.

For `crypt = ["TEN", "TWO", "ONE"]` and
```
solution = [['O', '1'],
            ['T', '0'],
            ['W', '9'],
            ['E', '5'],
            ['N', '4']]
```
the output should be
`isCryptSolution(crypt, solution) = false.`

Even though `054 + 091 = 145`, `054` and `091` both contain leading `zeroes`, meaning that this is not a valid solution.

### Input/Output

**[execution time limit]** 4 seconds (js)

**[input]** array.string crypt

An array of three non-empty strings containing only uppercase English letters.

**Guaranteed constraints:**
crypt.length = 3,
1 ≤ crypt[i].length ≤ 14.

**[input]** array.array.char solution

An array consisting of pairs of characters that represent the correspondence between letters and numbers in the cryptarithm. The first character in the pair is an uppercase English letter, and the second one is a digit in the range from 0 to 9.

It is guaranteed that solution only contains entries for the letters present in crypt and that different letters have different values.

**Guaranteed constraints:**
solution[i].length = 2,
'A' ≤ solution[i][0] ≤ 'Z',
'0' ≤ solution[i][1] ≤ '9',
solution[i][0] ≠ solution[j][0], i ≠ j,
solution[i][1] ≠ solution[j][1], i ≠ j.

**[output]** boolean

Return true if the solution represents the correct solution to the cryptarithm crypt, otherwise return `false`.

### Solution
```

const isCryptSolution = (crypt, solution) => {
    let mySolution = convertToObject(solution);
    let total = 0;

    for (let i=0;i<crypt.length-1;i++) {
        let result = getNumber(crypt[i], mySolution);
        if (result[0] === '0') {
            if(crypt[i].length > 1)
                return false;
            else
                return true;
        }
        
        total += parseInt(result, 10)
    }

    let final = getNumber(crypt[crypt.length-1], mySolution);
    if (final[0] !== '0') {
        if (total === parseInt(final, 10)) {
            return true;
        }
    }
    return false;
}

const getNumber = (s, map) => {
    let sum = '';

    for(let i=0;i<s.length;i++) {
        sum += map[s[i]];
    }

    return sum;
}

const convertToObject = arr => {
    let myObj = {};
    
    for(let i=0;i<arr.length;i++) {
        myObj[arr[i][0]] = arr[i][1];
    }
    
    return myObj;   
}
```

## Problem - Is beautiful string?

>A string is said to be _beautiful_ if `b` occurs in it no more times than `a`; `c` occurs in it no more times than `b`; etc.

Given a string, check whether it is _beautiful_.

**Example**

*   For `inputString = "bbbaacdafe"`, the output should be
    `isBeautifulString(inputString) = true`;
*   For `inputString = "aabbb"`, the output should be
    `isBeautifulString(inputString) = false`;
*   For `inputString = "bbc"`, the output should be
    `isBeautifulString(inputString) = false`.
*   For `inputString = "bbbaa"`, the output should be
    `isBeautifulString(inputString) = false`.
*   For `inputString = "bbbaaa"`, the output should be
    `isBeautifulString(inputString) = true`.


**Input/Output**

**[time limit] 4000ms (js)**

**[input] string inputString**

A string of lowercase letters.

_Guaranteed constraints:_
`3 ≤ inputString.length ≤ 50`.

**[output] boolean**

### Solution

```
var test = "bbbaacdafe"

const isBeautifulString = (s) => {
    let stringList = s.split("").sort(),
      alpha = "abcdefghijklmnopqrstuvwxyz".split(""),
      stringDict = {},
      values = [],
      unique = [],
      size = 0;
    
    if (stringList[0] !== 'a') {
      return false
    }
    
    for(let letter of stringList) {
      stringDict[letter] = stringDict[letter] + 1 || 1
    }
    
    values = Object.values(stringDict)
    unique = Object.keys(stringDict)
    size = values.length;
    
    for(let i = 0; i< size; i++) {
      if((i <= size - 1 && values[i] < values[i + 1] ) || unique[i] !== alpha[i])
        return false
    }
    
    return true
  }
```
