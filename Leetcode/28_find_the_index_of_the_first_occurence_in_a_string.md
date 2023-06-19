# 28. Find the Index of the First Occurrence in a String

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Example 1: 
```
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```

## Example 2: 
```
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```

## Constraints: 
```
1 <= haystack.length, needle.length <= 104
haystack and needle consist of only lowercase English characters.
```

## My Solution: 

The prompt does not specify that I cannot use built-in functions, so I went for a one-liner as below: 

```js
const strStr = (haystack, needle) => {
    return (!haystack.includes(needle) ? -1 : haystack.indexOf(needle));
}
```
Upon reading through the discussions, I noticed that some people didn't have the condition ```(!haystack.includes(needle))```. Sure enough, MDN shows that ```String.prototype.indexOf()``` returns -1 if the given substring is not found. Insignificant difference in performance unless the dataset is insanely large and a unique solution is guaranteed, but it will make the code simpler. 

```js
const strStr = (haystack, needle) => {
    return haystack.indexOf(needle);
}
```