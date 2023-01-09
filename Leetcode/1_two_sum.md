# 1. Two Sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target. 

You may assume that each input would have exactly one solution, and you may not use the same element twice. 

You can return the answer in any order.

## Example 1: 
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

## Example 2: 
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

## Example 3: 
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

## Constraints: 
```
2 <= nums.length <= 10^4
-10^9 <= nums[i] <= 10^9
-10^9 <= target <= 10^9
Only one valid answer exists.
```

**Follow-up:** Can you come up with an algorithm that is less than O(n2) time complexity?

## Notes
- Exactly one solution is guaranteed for each test case. 
- The input array *nums* is not necessarily ordered, so we cannot use two pointer unless we sort the array first. 
- There can be duplicate elements?? (i.e. [1, 9, 2, 5, 2, 7] with a target of 4) **Yes.**
- Will negative numbers affect the solution? **No.** 
- We are to return the indices of the two numbers. 

## Sample Solution 1: Brute Force
```js
var twoSum = function(nums, target) {
    for (let i = 0; i < nums.length-1; i ++) {
        for (let j = i + 1; j < nums.length; j ++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
}
```

## Sample Solution 2: Using an Object
```js
var twoSum = function(nums, target) {
    let hash = {};
    for(let i = 0; i < nums.length; i++) {
        const n = nums[i];
        if(hash[target - n] !== undefined) {
            return [hash[target - n], i];
        }
        hash[n] = i;
    }
}
```
- Create an empty object (key-value pair where key is the element and value is the index)
- Loop through each element of *nums* where *i* is the index and declare *n* as the value (nums[i]) at each iteration
- If the object does not contain a value that adds up to the target along with *n* at a given iteration, we add the index of *n* from nums into the object
- When the object contains a value that adds up to the target along with *n*, return both indexes

## Sample Solution 3: Two Pointers (if already sorted)
```js
var twoSum = function(nums, target) {
    let left = 0;
    let right = nums.length - 1;
    while(left < right) {
        let sum = nums[left] + nums[right];
        if(sum == target) {
            return [left, right];
        }
        else if(sum < target) {
            left += 1;
        }
        else {
            right -= 1;
        }
    }
}
```
