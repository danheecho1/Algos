# 509. Fibonacci Number 
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,
```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```
Given n, calculate F(n).

## Example 1:
```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

## Example 2:
```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

## Example 3: 
```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

## Constraints: 
```
0 <= n <= 30
```

## My Solution: 
This is a common question for a recursive function. The base cases are given as the definition of fibonacci number: F(0) = 0 and F(1) = 1. The recursive case is associated with the input integer n because F(n) = F(n-1) + F(n-2), and F(n-1) = F(n-2) + F(n-3) and so on. Recursion continues until we have n-1 = 1 and n-2 = 0 (two base cases), then recursion stops. 

```js
var fib = function fibo(n) {
    if(n === 0) return 0;
    if(n === 1) return 1;
    return fibo(n-1) + fibo(n-2);
}
```
Since the recursive case includes two calls for n, n-1, ... , 2, the time complexity is O(2^n). 