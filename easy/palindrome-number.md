# Palindrome Number – LeetCode #2 
**Link to the problem:** [Palindrome Number – LeetCode](https://leetcode.com/problems/palindrome-number/)  
---

## Problem Summary

Given an integer `x`, return `True` if `x` is a palindrome, and `False` otherwise.

A **palindrome** is a number that reads the same backward as forward.

**Example 1:**  
Input: `x = 121`  
Output: `True`

**Example 2:**  
Input: `x = -121`  
Output: `False`  
Explanation: From left to right, it reads `-121`, but from right to left: `121-`. So it's not the same.

**Example 3:**  
Input: `x = 10`  
Output: `False`

---
## My Thought Process
One of the easiest ways to solve this problem on LeetCode is by converting the number into a string. This allows us to treat the number like a sequence of characters and check whether it reads the same backward as forward. Here's what that looks like:

```python

def isPalindroome(x):
    x=str(x)
    return x==x[::-1]


```
What’s important to highlight here is the use of the slicing syntax `[::-1]`, which efficiently reverses the entire string.  
So when we compare `x` with `x[::-1]`, we're simply checking if the reversed version matches the original — the essence of a **palindrome**.

Although this solution is clean and readable, LeetCode introduces a follow-up challenge: solving the same problem **without converting the number to a string**.  
That’s where things get more interesting.

## Python Solution (Without Converting to String)

```python
def isPalindrome(x):
    if x < 0:
        return False
    temporal_list = []
    while x > 0:
        remainder = x % 10
        temporal_list.append(remainder)
        x = x // 10
    return temporal_list == temporal_list[::-1]
```
### Explanation

This solution avoids converting the integer to a string by working directly with its digits.

- First, we check if the number is negative. If it is, we immediately return `False`, since negative numbers cannot be palindromes (the minus sign will never match when reversed).
- We then extract the digits one by one using a mathematical trick:
  - The expression `x % 10` gives the **last digit** of the number.
  - We append that digit to a list called `temporal_list`. This means the **last digit of the number becomes the first element** in the list — effectively reversing the number as we go.
  - We update `x` by removing the last digit using integer division: `x = x // 10`.
- This process continues until the number is reduced to zero.

At the end, `temporal_list` contains all the digits of the number in **reverse order**.  
To check if the number is a palindrome, we compare the list with its reversed version using `temporal_list[::-1]`.

### Why `[::-1]` works

In Python, `[::-1]` is a slicing technique used to reverse sequences (like strings or lists).

- The full slice syntax is `[start:stop:step]`.
- Leaving `start` and `stop` empty and setting `step` to `-1` tells Python to return the sequence in **reverse order**.

So for a list like `[1, 2, 3]`, doing `[1, 2, 3][::-1]` returns `[3, 2, 1]`.



