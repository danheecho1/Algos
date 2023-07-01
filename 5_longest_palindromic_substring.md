# Longest Palindromic Substring

Given a string s, return the longest palindromic substring in s. 

## Example 1: 
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

## Example 2: 
```
Input: s = "cbbd"
Output: "bb"
```

## Constraints: 
```
1 <= s.length <= 1000
s consist of only digits and English letters.
```

## Initial Thoughts: 
My initial high-level pseudo code looked something like this: 
```
1) Examining all substrings within the given string and find all possible palindromic substrings  
2) Keep track of maxLength and maxLengthPal variables, and replace them as the code finds longer palindromic substring
3) Return the latest palindromic substring
```

I knew I could examine every substring combinations by using two for loops, and keeping track of the maximum length of a string was easy; I just needed to write a code that takes in each substring and checks whether the given substring was a palindrome or not. 

## My Inefficient Solution:
```js
const longestPalindrome = (s) => {
    const isPalindrome = (substring) => {
        let start = 0; 
        let end = substring.length - 1;
        while(start < end) {
            if(substring[start] !== substring[end]) {
                return false;
            } else {
                start ++;
                end --;
            }
        }
        return true;
    }
    let maxLengthPal = "";
    for(let i = 0; i < s.length; i ++) {
        for(let j = i; j < s.length; j ++) {
            let substring = s.slice(i, j+1);
            if(isPalindrome(substring) === true && substring.length > maxLengthPal.length) {
                maxLengthPal = substring;
            }
        }
    }
    return maxLengthPal;
};
```
I think this solution is O(n^3), but I'm not too certain. The nested for-loops already have O(n * n-1), and isPalindrome function is run for each iteration. isPalindrome function is O(substring.length/2), which can be O(n/2) at the worst case. O(n * n-1 * n/2) = O(n^3). 

## A Much Better Solution from the Solutions Section 
Not happy with my solution but unable to find a better way, I went to the solutions section and found *yupdduk*'s comment with the following solution: 
```js
var longestPalindrome = function(s) {
    let maxPal = '';

    for(let i = 0; i < s.length; i++) {
        bubble(i, i); // odd palindrome
        bubble(i, i + 1); // even palindrome
    }
    return maxPal;

    function bubble(left, right) {
        while(left >= 0 && s[left] === s[right]) {
            if(maxPal.length < right - left + 1) maxPal = s.slice(left, right + 1)
            left--;
            right++;
        }
    }
};
```
I couldn't understand what was going on here until I logged out the variables to see what was going on. 

```js
var longestPalindrome = function(s) {
    let maxPal = '';
    for(let i = 0; i < s.length; i++) {
        bubble(i, i); // odd palindrome
        bubble(i, i + 1); // even palindrome
    }
    return maxPal;

    function bubble(left, right) {
        console.log("left and right are", left, "and", right)
        console.log("s[left] is", s[left], "and s[right] is", s[right])
        console.log(left >= 0 && s[left] === s[right])
        while(left >= 0 && s[left] === s[right]) {
            console.log("maxPal before was", maxPal)
            if(maxPal.length < right - left + 1) maxPal = s.slice(left, right + 1)
            console.log("new maxPal is", maxPal)
            left--;
            right++;
            console.log("new left and right are", left, right)
        }
        console.log("------------------------------------------------------------------------")
    }
}

console.log(longestPalindrome("banana"))
```

This solution moves from index of 0 to the end of the given string. As it moves, it treats the current index as the center of the potential palindrome and checks its surrounding letters (if the surrounding letters on both sides are the same, palindrome!) The variable 'maxPal' is updated each time the bubble function runs and finds longer palindromic substring starting from the current center. Ultimately, we don't have to go through every single substring like we did with my solution. *yupdduk*'s solution runs in O(n^2) (for-loop at the top iterating from 0 to s.length, and the bubble function that can possibly run O(n/2) at the worst case if starting from the center of the substring). O(n * (n/2 + n/2)) = O(n^2)