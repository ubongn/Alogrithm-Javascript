# Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].



## Code
 ``````````````
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}


 const twoSum = (array, target) => {
    for ( let i = 0; i < array.length; i++) {
         for ( let j= i++; i< array.length; j++) {
              if ( array[j] === target - array[i]) return [i, j]               
         };
    };
    return null;
};


