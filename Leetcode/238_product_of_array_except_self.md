# 238. Product of Array Except Self 
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

## Example 1:
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

## Example 2:
```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

## Constraints: 
```
2 <= nums.length <= 10^5
-30 <= nums[i] <= 30
The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
```

**Follow up:** Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

## Notes
- Will create an array of the same length as the input array. Fill it with 1's. This array will be returned as the solution. 
- The key is to separate left and right sides of nums[i]. For example, if nums = [1, 2, 3, 4, 5], consider that we have (1), [1, 2, 3, 4, 5], (1). At i = 0, left will be 1, and right will be 2 * 3 * 4 * 5 * 1 = 120. At i = 1, left will be 1 * 1 = 1, and right will be 3 * 4 * 5 * 1 = 60. 
- We will have one loop over the input array, calculating left at each index. Each left value will be pushed into the array we created in the beginning. 
- We will have another loop over the input array, but in reverse order. This time, we calculate right at each index. Each right value will be multiplied to what we pushed into the output array from the previous step. 

## Sample Solution: 
```js
var productExceptSelf = function(nums) {
    let left = 1;
    let right = 1;
    let result = new Array(nums.length).fill(1);
    for(let i = 0; i < nums.length; i ++) {
        result[i] *= left;
        left *= nums[i];
    }
    for(let i = nums.length - 1; i >= 0; i --) {
        result[i] *= right;
        right *= nums[i];
    }
    return result;
};
```