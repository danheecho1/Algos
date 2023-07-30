# 268. Missing Number
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

## Example 1: 
```
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
```

## Example 2: 
```
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
```

## Example 3: 
```
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.
```

## Constraints: 
```
n == nums.length
1 <= n <= 10^4
0 <= nums[i] <= n
All the numbers of nums are unique.
```

**Follow up**: Could you implement a solution using only O(1) extra space complexity and O(n) runtime complexity? 

## Thought Process / Pseudo

- Create an array with length nums.length + 1 (nums.length is missing one item that we need to return), and fill it with "answer". 
- Loop through the input array (not the new array we just created). 
  - New array at index of nums[i] will be assigned the value of nums[i]. 
  - The end result of this loop will be an array with numbers 0 to n in order, except for the missing number that still reads "answer". 
- Return the index of "answer". 

## Solution

```js
var missingNumber = function(nums) {
    let collectionArr = new Array(nums.length + 1).fill("answer");
    for(let i = 0; i < nums.length; i ++) {
        collectionArr[nums[i]] = nums[i];
    }
    return collectionArr.indexOf("answer");
};
```
This solution has time complexity of o(n) (for loop and indexOf are linear, not nested) and space complexity of o(n) (collectionArr grows proportionate to the size of nums). 

The follow up question asked for a solution with o(1) space complexity, but I could not figure out how on my own. 

## ChatGPT Delivers
Consulting with ChatGPT again, I learned that this problem can be solved using bitwise XOR again (crazy)! The idea is to perform XOR on all elements from the input array as well as their indexes. Given that all numbers in the input array are unique and ranges from 0 to n, we should end up with pairs of indexes and their matching values except for the missing number. 

- For example, if we have an input array of [0, 1, 2, 4]: 
  - Because the array has 4 numbers, it should range from 0 to 4 meaning it has 5 numbers. 
  - What should have been = [0, 1, 2, 3, 4]. What we are given = [0, 1, 2, 4]. We need to identify that missing 3. 
  - We will be bitwise XORing the following numbers: 
    - Index of 0, 1, 2, 3, and 4 because we're supposed to have 5 numbers. 
    - Numbers we have in the input array: 0, 1, 2, and 4
    - Result = (0 ^ 1 ^ 2 ^ 3 ^ 4) ^ (0 ^ 1 ^ 2 ^ 4) = 3

```js
var missingNumber = function(nums) {
  let result = nums.length;
  for(let i = 0; i < nums.length; i ++) {
    result ^= i ^ nums[i];
  }
  return result;
}
```