# 26. Remove Duplicates from Sorted Array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.
Custom Judge:

The judge will test your solution with the following code:
```
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be accepted.

## Example 1: 
```
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

## Example 2: 
```
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

## Constraints: 
```
1 <= nums.length <= 3 * 104
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order.
```

## Thoughts and Solutions: 
This problem asks to mutate the input array by deleting duplicate values AND return the number of unique values. I was not sure how to rotate parts of an array upon finding duplicate values (proof that I have not done a lot of algo practices), so I went for creating a new array that only included unique values from the input array. Then, I copied the unique values to the input array. Examples state that it does not matter what I leave beyond the returned unique values in the array. 
```js
const removeDuplicates = (nums) => {
    let expectedNums = [];
    let hash = {}; 
    for(let i = 0; i < nums.length; i ++) {
        if(hash[nums[i]] === undefined) {
            expectedNums.push(nums[i]);
        }
        hash[nums[i]] = 1;
    }
    for(let i = 0; i < expectedNums.length; i++) {
        nums[i] = expectedNums[i];
    }
    return expectedNums.length;
};
```

Then, I asked chatGPT to solve the same problem. 
```js
function removeDuplicates(nums) {
    let i = 0;
    for (let j = 1; j < nums.length; j++) {
        if (nums[j] !== nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```
Wow 1: This was a two-pointer problem? (I need more algo in my life)

Wow 2: My solution is O(n) too, but only because I get to omit constants.. This has to be much faster than my solution!

I knew my solution was going through some unnecessary steps, but I didn't realize that I was making it that much more complicated. 