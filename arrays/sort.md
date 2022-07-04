## Understanding the problem
Given an array of integers that are sorted in increasing order, we are asked to write a function that squares all the integers in the array and returns them in a new array. The returned array must be sorted in increasing order as well.

## APPROACH
At first glance, we might think all we need to do is traverse the input array element by element, square each value and return the resultant array.

However, this approach only works for positive integers.

Negative numbers become positive when squared. If we put them directly into the resultant array, the array would no longer be sorted. We could sort the resultant array before returning it, but then the solution will take O(N · log(N)) time.

Instead of sorting, we can store the squares of non-negative and negative integers separately by using two arrays. After squaring all the integers, we merge the two arrays into one sorted array:

Let m be the length of the first array and n be the length of the second array. Initialize an empty array merged of length m + n.

Initialize two pointers that are going to remember the position we are at in the two arrays respectively. Point the pointer for the non-negative array to the first number of the array, and the one for the negative array to the last number of the array. The reason for that is because smaller negative numbers become bigger after squaring, and since the input array is sorted in ascending order, the squares of all the negative numbers will be in descending order.

Iterate through the merged array. At each iteration, we compare the values that the two pointers are pointing to. Put the smaller value into merged[i] and move the corresponding pointer. To handle the situation where the end of one of the arrays is reached, we can set the corresponding value to a very large number.


```
function sortedSquaredArray(array) {
  const positiveSquares = [];
  const negativeSquares = [];

  for (const value of array) {
    const square = value * value;

    if (value < 0) {
      negativeSquares.push(square);
    } else {
      positiveSquares.push(square);
    }
  }

  return mergeSortedArrays(positiveSquares, negativeSquares);
}

function mergeSortedArrays(ascendingArray, descendingArray) {
  const merged = new Array(ascendingArray.length + descendingArray.length);
  let ascendingIdx = 0;
  let descendingIdx = descendingArray.length - 1;

  for (let i = 0; i < merged.length; i++) {
    const ascendingItem = ascendingArray[ascendingIdx] ?? Infinity;
    const descendingItem = descendingArray[descendingIdx] ?? Infinity;

    if (ascendingItem < descendingItem) {
      merged[i] = ascendingItem;
      ascendingIdx++;
    } else {
      merged[i] = descendingItem;
      descendingIdx--;
    }
  }

  return merged;
}
```


```function sortedSquaredArray(array) {
  const sortedSquares = new Array(array.length);
  let smallerValueIdx = 0;
  let largerValueIdx = array.length - 1;

  for (let i = array.length - 1; i >= 0; i--) {
    const smallerValue = array[smallerValueIdx];
    const largerValue = array[largerValueIdx];

    if (Math.abs(smallerValue) >= Math.abs(largerValue)) {
      sortedSquares[i] = smallerValue * smallerValue;
      smallerValueIdx++;
    } else {
      sortedSquares[i] = largerValue * largerValue;
      largerValueIdx--;
    }
  }

  return sortedSquares;
}