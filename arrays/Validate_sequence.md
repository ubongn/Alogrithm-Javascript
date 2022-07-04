## Understanding the problem
We are given two arrays of integers array and sequence. We are asked to implement a function that is going to check whether all the numbers in the sequence appear in the array and they appear in the same order. In other words, the function needs to find out if we can get the sequence array from the array, when we delete some or no elements in the array without changing the order of the remaining elements.

Example:

```
array: [3, 1, 7, 5, 10, 2];
sequence: [1, 5, 2];
Output: true

```
# 1
We can use a pointer to remember the position we are at in the sequence array. Iterate through the array. At each iteration, compare the current element in the array to the element that the pointer is pointing at. If they are equal to each other, then it means the element in the sequence does appear in the array, move the pointer forward by 1. If the pointer is equal to the length of the sequence array, then it means all the elements in the sequence array are found in the array and they are in the same order, return true. When we get out of the loop without returning the result, return false.

```
function isValidSubsequence(array, sequence) {
  let seqIdx = 0;
  for (const value of array) {
    if (value === sequence[seqIdx]) seqIdx++;
    if (seqIdx === sequence.length) return true;
  }

  return false;
}
```

# 2

```
function isValidSubsequence(array, sequence) {
  let arrIdx = 0;
  let seqIdx = 0;

  while (arrIdx < array.length && seqIdx < sequence.length) {
    if (array[arrIdx] === sequence[seqIdx]) {
      seqIdx++;
    }
    arrIdx++;
  }

  return seqIdx === sequence.length;
}
```