# 14. Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

## Example 1: 
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

## Example 2: 
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Constraints: 
```
1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lowercase English letters.
```

## My Thought Process 
The most obvious edge case was when the input array would have only one item in it. In this case, I would return that item as a whole string. 
```js
if(strs.length === 1) return strs[0];
```
At first, I thought of nested loops so that I could iterate over each letter of each element within the given array - that was no good. Not only would it have been a slow solution (O(n)<sup>2</sup>), but I also struggled with how to keep track of the letter I was checking against across all elements in the array. 

Then, I thought of using array's reduce method as I reminded myself that I would be taking in an array and returning a single string, and I think that was a good approach. Reduce method iterates through all elements within an array, and I could create another conditional variable to track the number of letters that are shared as prefix among all words. 

## Solution: 
```js
const longestCommonPrefix = (strs) => {
    if(strs.length === 1) {
        return strs[0];
    }
    let answer = strs.reduce((prev, curr) => {
        let i = 0; 
        while(prev[i] && curr[i] && (prev[i] === curr[i])) {
            i ++;
        } 
        return prev.slice(0, i);
    })
    return answer;
}
```