# Understanding the problem

Given an array of distinct integers and an integer representing the target sum, we are asked to implement a function that is going to find out whether there's a pair of numbers in the array that adds up to the target sum. If such pair exists, return the pair in any order; otherwise return an empty array. We cannot add a number to itself to get the target sum.

## 1: Brute Force
Iterate through the array. For each number, iterate through the rest of the array; if adding any number in the rest of the array to the number yields the target sum, return the pair.

```
function twoNumberSum(array, targetSum) {
  for (let i = 0; i < array.length; i++) {
    const firstNum = array[i];
    for (let j = i + 1; j < array.length; j++) {
      const secondNum = array[j];
      if (firstNum + secondNum === targetSum) {
        return [firstNum, secondNum];
      }
    }
  }

  return [];
}
```

## **Complexity Analysis**

* **Time Complexity:** O(N^2), where N is the length of the input array.

* **Space Complexity:** O(1).

## 2: Two Pass with Hash Table
In the brute force approach above, the repeated search for each number's complement (target sum - array[i]) slows down the overall runtime. We can reduce the search from O(N) to amortized O(1) by throwing all the number in the array into a hash table, trading space for time. We need to ensure that the complement is not the current number itself though. For instance, suppose the input array is [5, 2] and the target sum is 10, the hash table is going to be {5: value, 2: value}. The complement of 5 is 5 (10 - 5 = 5) and 5 does exist in the hash table, however, the complement is the number itself, thus it is not a valid answer. To handle this we can store each number's index as value in the hash table and compare the complement's index to the current number's index.

### **Algorithm**

* Go through the input array. Add each number as key and its index as value to the hash table.

* Loop through the input array again. Check if each number's complement is present in the hash table. If it is present and is not the current number itself, return the current number and its complement.

```
function twoNumberSum(array, targetSum) {
  const hashTable = new Map();

  for (let i = 0; i < array.length; i++) {
    hashTable.set(array[i], i);
  }

  for (let i = 0; i < array.length; i++) {
    const complement = targetSum - array[i];

    if (hashTable.has(complement) && hashTable.get(complement) !== i) {
      return [array[i], complement];
    }
  }

  return [];
}
```

### ***Complexity Analysis***
* **Time Complexity**: O(N^2), where N is the length of the input array.

* **Space Complexity**: O(1).


## 3: One Pass with Hash Table
We can check if the complement of the current number is present in the hash table while we are adding numbers into the hash table. At each step, we first look up current number's complement in the hash table. If it already exists, then we have found the pair; otherwise, add the current number into the hash table.

```
function twoNumberSum(array, targetSum) {
  const hashTable = new Map();

  for (const num of array) {
    const complement = targetSum - num;

    if (hashTable.has(complement)) {
      return [complement, num];
    }

    hashTable.set(num, true);
  }

  return [];
}
```

### ***Complexity Analysis***
Let N be the length of the input array.

* **Time Complexity**: O(N).

* **Space Complexity**: O(N).


## 4: Sort + Two Pointers
We sort the input array in ascending order and use two pointers to find the pair in the array.

Suppose the input array is [5, 1, -2, 6, -4, 9] and the target sum is 3. After sorting the array, we get [-4, -2, 1, 5, 6, 9].
We initialize two pointers l and r to point to the first and last elements in the array respectively.

```
function twoNumberSum(array, targetSum) {
  array.sort((a, b) => a - b);

  let left = 0;
  let right = array.length - 1;

  while (left < right) {
    const currSum = array[left] + array[right];
    if (currSum === targetSum) {
      return [array[left], array[right]];
    }
    if (currSum < targetSum) {
      left++;
    } else {
      right--;
    }
  }

  return [];
}
```

### ***Complexity Analysis***
* **Time Complexity**: O(N · log(N)), where N is the length of the input array.

* **Space Complexity**: O(log(N)) or O(N), depending on the implementation of the sorting algorithm.
