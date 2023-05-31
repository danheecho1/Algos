# 13. Roman to Integer
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

- I can be placed before V (5) and X (10) to make 4 and 9. 
- X can be placed before L (50) and C (100) to make 40 and 90. 
- C can be placed before D (500) and M (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

## Example 1: 
```
Input: s = "III"
Output: 3
Explanation: III = 3.
```

## Example 2: 
```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

## Example 3: 
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Constraints: 
```
- 1 <= s.length <= 15
- s contains only the characters ('I', 'V', 'X', 'L', 'C', 'D', 'M').
- It is guaranteed that s is a valid roman numeral in the range [1, 3999].
```

## Initial Questions
- Would there ever be a case where there are multiple I's before V or X, or multiple X's before L or C, and so on? (i.e. would IIV equal 3?) 
  - No. For example, 3 would be III, not IIV. 
- What's the purpose of the third constraints - that the roman numeral goes up to 3999? 
  - Numbers 4000 and above require vinculum (line above the roman numerals) to indicate that the number is multiplied by 1000. Maybe it's too complicated to have numbers with vinculum in this algo? 

## Initial Thought Process
I wanted to start by creating an object with the roman numerals and their respective values, as well as a variable to keep track of the running sum which would eventually end up being the number that the roman numerals represent as a whole. I got this far with no problem: 
```js
const map = {
    "I": 1, 
    "V": 5, 
    "X": 10, 
    "L": 50, 
    "C": 100, 
    "D": 500, 
    "M": 1000
}
let sum = 0;
```
My initial plan of attack was to identify the first instance of the highest roman numeral, and check if there is any other roman numeral before that instance. If there was nothing, I would simply add the roman numeral's value to the sum. If there was anything before the highest roman numeral, I would subtract it from the highest roman numeral, and then add the difference to the sum variable. Once the if-statement chains were completed, I would slice the input string so that the first instance of the highest roman numeral and anything to the left of it would be chopped. Repeating these steps until the input string was empty should have given me the answer, but I wasn't able to code it out. I kept seeing that my logic didn't make sense, but I didn't know how to make it work. 

I didn't want to spend all day on this one problem, so I googled how roman numerals worked. The logic was way simpler than I made it to be. https://www.tutorialspoint.com/p-how-to-write-5000-in-roman-numbers-p#:~:text=For%20numbers%20over%201%2C000%2C%20you,numerals%20is%20%E2%80%BEVV handed me the logic in two sentences: 1) If smaller numbers follow larger numbers, add the numbers, and 2) if a smaller number precedes a larger number, subtract the smaller number. After testing this logic with a few seemingly complicated numbers by hand, I realized that all there is to roman numeral is a combination of addition and subtraction. 

III is equivalent to I + I + I = 1 + 1 + 1. LVIII is equivalent to L + V + I + I + I = 50 + 5 + 1 + 1 + 1. MCMXCIV can be looked as M(CM)(XC)(IV) => M + (-C + M) + (-X + C) + (-I + V) = M - C + M - X + C - I + V = 1994. This realization led to a very simple solution as below: 
```js
const romanToInt = (s) => {
    const map = {
        "I": 1, 
        "V": 5, 
        "X": 10, 
        "L": 50, 
        "C": 100, 
        "D": 500, 
        "M": 1000
    }
    let sum = 0;
    for(let i = 0; i < s.length; i++) {
        map[s[i]] < map[s[i+1]] ? sum -= map[s[i]] : sum += map[s[i]];
    }
    return sum;
};
```
