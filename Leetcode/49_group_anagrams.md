# 49. Group Anagrams
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Example 1: 
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

## Example 2: 
```
Input: strs = [""]
Output: [[""]]
```

## Example 3: 
```
Input: strs = ["a"]
Output: [["a"]]
```

## Constraints: 
```
1 <= strs.length <= 10^4
0 <= strs[i].length <= 100
strs[i] consists of lowercase English letters.
```

## Notes
- If the length of the input array is 1, return the array itself. 
- Output will be an array of arrays of anagrams. 
- No guarantee that the length of the words within the given array is the same.. Is that a good thing or a bad thing? 

## Sample Solution 1: 
```js
var groupAnagrams = function(strs) {
    // Create an object to store character counts as keys and lists (arrays) of words from 'strs' as values
    let map = {};
    // Loop through each word given in 'strs'
    for(let i = 0; i < strs.length; i++) {
        // Create a new 'count' array of 26 zeros representing the alphabet
        const count = new Array(26).fill(0);
        // Declare a variable for the word that the loop is currently on, so that we can..
        const word = strs[i];
        // Loop through the characters in the word
        for(let j = 0; j < word.length; j++) {
            // Find the unicode decimal corresponding to the letter or the alphabet in the ascii code, then subtract the unicode decimal for 'a' so that 'a' would result in 0, 'b' would result in 1, and so on. The resulting number would be the index of the 'count' array which is filled with 26 zeroes. 
            // At the end of this loop, we should have an array of numbers indicating the number of occurences of each letter in order from a to z. 
            count[ word.charCodeAt(j) - "a".charCodeAt(0) ] += 1;
        }
        // If the specific count array is already in the map object as a key, then we add the word we just worked on as one of the values. Note that we are using push method; the values here are arrays. If the count array does not exist in the map object yet, we simply create a key using the count array, and add an array including the word as the value.
        if(count in map) {
            map[count].push(word);
        } else {
            map[count] = [word];
        }  
    }
    // Finally, we return the values of the map. 
    return Object.values(map);
}
```
