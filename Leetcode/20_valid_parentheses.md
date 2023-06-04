# 20. Valid Parentheses
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.

Open brackets must be closed in the correct order.

Every close bracket has a corresponding open bracket of the same type.

## Example 1: 
```
Input: s = "()"
Output: true
```

## Example 2: 
```
Input: s = "()[]{}"
Output: true
```

## Example 3: 
```
Input: s = "(]"
Output: false
```

## Constraints: 
```
1 <= s.length <= 104
s consists of parentheses only '()[]{}'.
```

## My Solution
```js
const isValid = (s) => {
    if(s.length % 2 === 1) {
        return false;
    }

	const pairs = {
		"(": ")",
		"{": "}",
		"[": "]",
	};
    let toBeResolved = [];

    for(let i = 0; i < s.length; i++) {
        if(Object.keys(pairs).includes(s[i])) {
            toBeResolved.push(s[i]);
        }
        else {
            if(toBeResolved.length === 0) {
                return false;
            }
            else if(pairs[toBeResolved[toBeResolved.length - 1]] === s[i]) {
                toBeResolved.pop();
                continue;
            } else {
                return false;
            }
        }
    }
    if(toBeResolved.length === 0) {
        return true;
    }
    else {
        return false;
    }
};
```

