# Reverse Integer
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

## Example 1:
```
Input: x = 123
Output: 321
```

## Example 2:
```
Input: x = -123
Output: -321
```

## Example 3:
```
Input: x = 120
Output: 21
```

## My Solution: 
```js
const reverse = (x) => {
	let input = x;
	let output = 0;
	while (Math.abs(input) > 0) {
		let temp = Math.abs(input) % 10;
		output = output * 10 + temp;
		if (input >= 0) {
			input = Math.floor(input / 10);
		} else {
			input = Math.ceil(input / 10);
		}
	}
	if (output > Math.pow(2, 31) - 1 || output < Math.pow(-2, 31)) {
		return 0;
	}
	if (x < 0) {
		return output * -1;
	}
	return output;
};
```