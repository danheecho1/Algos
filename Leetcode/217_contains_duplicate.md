# 217. Contains Duplicate
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

## Example 1: 
```
Input: nums = [1,2,3,1]
Output: true
```

## Example 2:
```
Input: nums = [1,2,3,4]
Output: false
```

## Example 3: 
```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

## Constraints: 
```
1 <= nums.length <= 10^5
-10^9 <= nums[i] <= 10^9
```

## Notes
- Output is boolean; no need for index values. 

## Sample Solution 1: Brute Force
```js
var containsDuplicate = function(nums) {
	for(let i = 0; i < nums.length; i++) {
		for(let j = i + 1; j < nums.length; j++) {
			if(nums[i] == nums[j]) {
				return true;
			}
		}
	}
	return false;
}
```

## Sample Solution 2: Using Object
```js
var containsDuplicate = function(nums) {
	// Create an object called 'checklist'
	let checklist = {};
	// Loop through the input array 'nums'
	for(let i = 0; i < nums.length; i++) {
		// If checklist does not have nums[i] as a key yet, add a key-value pair of nums[i] : 1
		if(checklist[nums[i]] == undefined) {
			checklist[nums[i]] = 1;
		}
		// If checklist already has nums[i] as a key, it is a duplicate; return true 
		else {
			return true;
		}
	}
	// If we have not returned true yet and exited the for-loop, we have not had a duplicate yet; return false
	return false;
}
```
