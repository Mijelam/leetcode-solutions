# Valid Parentheses  -LeetCode #5

**Link to the problem:** [Valid Parentheses – LeetCode](https://leetcode.com/problems/valid-parentheses)

## Problem Summary

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid.

An input string is valid if:
- Open brackets are closed by the same type of brackets.
- Open brackets are closed in the correct order.

### Examples:

**Input:** `"()"`  
**Output:** `true`

**Input:** `"()[]{}"`  
**Output:** `true`

**Input:** `"(]"`  
**Output:** `false`

## Python Solution

```python
def isValid(self, s: str) -> bool:
    while any(p in s for p in ["()", "[]", "{}"]): 
        s = s.replace("()", "").replace("[]", "").replace("{}", "") 
    return s == ""
```

## My Thought Process

I chose a very intuitive approach: as long as we keep finding valid pairs of brackets like `"()"`, `"[]"`, or `"{}"` inside the string, we remove them. This continues until no such pairs remain. If the string is completely reduced to an empty string, it means all brackets were matched and closed properly, so the input is valid. Otherwise, some unmatched brackets remain and the string is invalid.

This method relies on the idea that valid parentheses will always eventually collapse into nothing if removed in pairs.

## Explanation

This solution repeatedly removes any directly matching pairs of brackets from the string—specifically `"()"`, `"[]"`, and `"{}"`. It uses a `while` loop that continues to check for the presence of these valid pairs and removes them using the `replace` method.

The loop stops when none of those pairs exist in the string anymore. At that point, if the string is empty, it means all parentheses were correctly matched. If anything remains in the string, it indicates that there were unmatched or incorrectly ordered brackets, so the function returns `False`.
