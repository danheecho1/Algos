# 136. Single Number
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## Example 1: 
```
Input: nums = [2,2,1]
Output: 1
```

## Example 2:
```
Input: nums = [4,1,2,1,2]
Output: 4
```
## Example 3: 
```
Input: nums = [1]
Output: 1
```

## Constraints: 
```
1 <= nums.length <= 3 * 10^4
-3 * 10^4 <= nums[i] <= 3 * 10^4
Each element in the array appears twice except for one element which appears only once.
```

## Thought Process / Pseudo
- Loop through the input array
- Use Array.prototype.shift() to remove the first item from the array and store it in a temporary variable
- Use Array.prototype.indexOf() to check if the temporary value stored from the previous step is found in the remaining array
- If the value is not found in the remaining array, return the value
- If the value is found in the remaining array, use Array.prototype.splice() to remove the duplicate that is found in the remaining array, and start from the top of the loop

This solution has a time complexity of o(n^2) for the for loop and indexOf(). I didn't realize it was o(n^2) until I submitted my code to Leetcode and saw that the response took too long. I thought it was o(n) because I loop through the array once. 

```js
const singleNumber = (nums) => {
	let copy = [...nums];
	for (let i = 0; i < nums.length; i++) {
		let test = copy.shift();
		let testIndex = copy.indexOf(test);
		if (testIndex !== -1) {
			copy.splice(testIndex, 1);
			continue;
		} 
		return test;
	}
};
```

After looking at others' solutions, I came across bitwise XOR operation. It took me a long time to understand what was going on, but it blew my mind once I understood. 
- Bitwise operator (^) converts two numbers into their binary representations and returns the **difference**. 
- What it means by return the 'difference' is... 
  - Once the two numbers are converted into their binary representations, each digit from both numbers will be compared. If both digits are the same (0 and 0, or 1 and 1), we end up with 0. If both digits are different (0 and 1, or 1 and 0), we end up with 1. 
  - For example... 
    ```js
    const a = 3;        // 0 0 0 0 0 1 1
    const b = 4;        // 0 0 0 0 1 0 0
    console.log(a ^ b); // 0 0 0 0 1 1 1
    ```
- What do we do with this to find a unique value without a pair? Performing bitwise XOR operation on the two same numbers will always result in 0. 
  - For example... 
    ```js
    const a = 3;        // 0 0 0 0 0 1 1
    const b = 3;        // 0 0 0 0 0 1 1
    console.log(a ^ b); // 0 0 0 0 0 0 0
    ```
  - If we were to perform XOR operation on multiple numbers including one pair of the same number, those two numbers would cancel each other out and have no net effect on the result. 
    - For example... 
    ```js
    const a = (3 ^ 1 ^ 1 ^ 4);
    //      3: 0 0 0 0 0 1 1
    //      1: 0 0 0 0 0 0 1
    //      1: 0 0 0 0 0 0 1
    //      4: 0 0 0 0 1 0 0
    // result: 0 0 0 0 1 1 1

    const b = (3 ^ 4);
    //      3: 0 0 0 0 0 1 1
    //      4: 0 0 0 0 1 0 0
    // result: 0 0 0 0 1 1 1

    console.log(a === b) // true
    ```
- We know that the input array will have values in pairs except for one value. All values in pairs will not have any net effect on the bitwise operation we perform.. So all we need to do is just perform bitwise XOR on every single element from the input array. What's left will be a binary representation of the unique value. 
  - For example...
  ```js
  const inputArray = [1, 3, 5, 1, 3];
  const testA = (1 ^ 3 ^ 5 ^ 1 ^ 3);
  const testB = 5;
  ```

## Final Solution 
Using the bitwise XOR as described above, we have the following solution: 
```js
const singleNumber = (nums) => {
    let result = 0;
    for(let i = 0; i < nums.length; i++) {
        result = result ^ nums[i]; // or result ^= nums[i], but it looks a bit awkward to my eyes seeing bitwise xor for the first time
    }
    return result;
}
```

This solution has o(n) time complexity to go through the input array once, and o(1) space complexity. 

## Credit
- https://www.youtube.com/watch?v=XzQSPg6LFyY&ab_channel=ALGOBYTE

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_XOR
