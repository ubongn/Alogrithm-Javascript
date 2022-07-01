# Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.





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


