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
