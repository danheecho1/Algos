# Letter Combinations of a Phone Number

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```js
const hash = {
	2: ["a", "b", "c"],
	3: ["d", "e", "f"],
	4: ["g", "h", "i"],
	5: ["j", "k", "l"],
	6: ["m", "n", "o"],
	7: ["p", "q", "r", "s"],
	8: ["t", "u", "v"],
	9: ["w", "x", "y", "z"],
};
```

## Example 1:

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

## Example 2:

```
Input: digits = ""
Output: []
```

## Example 3:

```
Input: digits = "2"
Output: ["a","b","c"]
```

## Constraints:

```
0 <= digits.length <= 4
digits[i] is a digit in the range ['2', '9'].
```

## Solution:

```js
const letterCombinations = (digits) => {
	// If no number is pressed, it cannot form any word
	if (digits.length === 0) return [];

	// Map out all the letters to each number
	const hash = {
		2: ["a", "b", "c"],
		3: ["d", "e", "f"],
		4: ["g", "h", "i"],
		5: ["j", "k", "l"],
		6: ["m", "n", "o"],
		7: ["p", "q", "r", "s"],
		8: ["t", "u", "v"],
		9: ["w", "x", "y", "z"],
	};

	// The digits pressed are separated individually and added to an array
	const inputList = digits.split("");
	// Result will be where we keep the running list of all possible letter combinations
	let result = [""];

	// We loop through each digit pressed
	for (let i = 0; i < inputList.length; i++) {
		// Find the letters corresponding to the digit that we are looping through 
		const letters = hash[inputList[i]];
		// Temporary array where we save the result array modified by below nested for loops
		const temp = [];
		// We loop through each combination that we have in the result array. The very first iteration, we loop over an empty string. 
		for (let j = 0; j < result.length; j++) {
			// For each existing combination, add a new letter and push the result to temp array
			for (let k = 0; k < letters.length; k++) {
				temp.push(result[j] + letters[k]);
			}
		}
		// Save the final temp array as new result which will be used again in the next loop cycle
		result = temp;
	}
	return result;
};
```
