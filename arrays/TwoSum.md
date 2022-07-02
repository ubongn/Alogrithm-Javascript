# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].



## Code
 ```
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}


 const twoSum = (array, target) => {
    for ( let i = 0; i < array.length; i++) {
         for ( let j = i++; i< array.length; j++) {
              if ( array[j] === target - array[i]) 
              return [i, j]               
         };
    };
    return null;
};

```

## This was accepted

```

 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}

const twoSum = (nums, target) => {
  const previousValues = {}
  for (let i = 0; i < nums.length; i++) {
    const currentValue = nums[i]
    const neededValue = target - currentValue
    if (previousValues[neededValue] != null) {
      return [previousValues[neededValue], i]
    } else {
      previousValues[currentValue] = i
    }
  }

	return []
}
```
```
const twoSum = (nums, target) => {
    const prevValues = {}
    for (let i = 0; i < nums.length; i++){
        const currentNumber = nums[i]
        const neededValue = target - currentNumber
        const index2 = prevValues[neededValue]
        if(index2 != null){
            return [index2, i]
        }else {
            prevValues[currentNumber] = i
        }
    }
    return null
}