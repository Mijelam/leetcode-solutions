# Find the Index of the First Occurrence in a String # 8

[Link to the problem](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

## Problem Summary

Given two strings `haystack` and `needle`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

**Example 1:**  
Input: haystack = "sadbutsad", needle = "sad"  
Output: 0

**Example 2:**  
Input: haystack = "leetcode", needle = "leeto"  
Output: -1

## Python Solution

```python
def strStr(self, haystack: str, needle: str) -> int:
    length_ndle = len(needle)
    length_hystk = len(haystack)
    for i in range(length_hystk - length_ndle + 1):
        if haystack[i:i+length_ndle] == needle:
            return i
    return -1
```

## My Thought Process

Although the solution is simple, it requires a deep understanding of the problem. When analyzing the first test case — `haystack = "sadbutsad"` and `needle = "sad"` — I realized that I needed to iterate over the `haystack` string and compare slices of it with `needle`. This led me to design a `for` loop that moves one character at a time through `haystack`, comparing substrings of the same length as `needle`. If a match is found, I return the current index. If no match is found by the end of the loop, I return `-1`.

## Explanation

We first calculate the lengths of both `needle` and `haystack`. Then, we iterate from index 0 to `length_hystk - length_ndle`, inclusive. This ensures that we only compare substrings that are long enough to contain `needle`.

In each iteration, we take a slice of `haystack` starting at index `i` with the length of `needle` and check if it equals `needle`. If a match is found, we return the current index `i`. If the loop finishes without finding a match, we return `-1`.
