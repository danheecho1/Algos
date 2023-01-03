# 242. Valid Anagram
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Example 1: 
```
Input: s = "anagram", t = "nagaram"
Output: true
```

## Example 2: 
```
Input: s = "rat", t = "car"
Output: false
```

## Constraints: 
```
1 <= s.length, t.length <= 5 * 10^4
s and t consist of lowercase English letters.
```

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Sample Solution 1: Using Object
```js
var isAnagram = function(s, t) {
	if(s.length != t.length) {
		return false;
	}
	let lettersInS = {};
	let lettersInT = {};
	for(let i = 0; i < s.length; i++) {
		if(lettersInS[s[i]] == undefined) {
			lettersInS[s[i]] = 1;
		} else {
			lettersInS[s[i]] += 1;
		}
	}
	for(let j = 0; j < t.length; j++) {
		if(lettersInT[t[j]] == undefined) {
			lettersInT[t[j]] = 1;
		} else {
			lettersInT[t[j]] += 1;
		}
	}
	for(let k = 0; k < s.length; k ++) {
		if(lettersInS[s[k]] != lettersInT[s[k]]) {
			return false;
		}
	}
	return true;
}
```

## Sample Solution 2: Solution posted by Pigpigever (08.23.17)
```js
var isAnagram = function(s, t) {
    if(s.length !== t.length){
        return false;
    }
    s = s.split('').sort().join('');
    t = t.split('').sort().join('');
	return (s == t ? true : false);
}
```