# 13. Roman to Integer

**Link to the problem:** [Roman To Integer - LeetCode](https://leetcode.com/problems/roman-to-integer/)


## Problem Summary

Given a Roman numeral, convert it to an integer.

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D`, and `M`.

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

---

## Python Solution

```python
def romanToInt(self, s: str) -> int:
    Roman_dict = {
        "I": 1,
        "V": 5,
        "X": 10,
        "L": 50,
        "C": 100,
        "D": 500,
        "M": 1000
    }
    
    number = 0
    length_input = len(s)
    i = 0
    while i < length_input:
        current_value = Roman_dict[s[i]]
        next_value = Roman_dict[s[i + 1]] if i < length_input - 1 else 0
        if current_value < next_value:
            number += next_value - current_value
            i += 2
        else:
            number += current_value
            i += 1
    return number
```
## My Thought Process

At first, it was very clear to me that I needed to use a dictionary, because the structure of the problem naturally maps Roman symbols to their numeric values. So I started by creating a dictionary where each Roman numeral is a key, and its corresponding integer value is the value.

Next, I analyzed simple cases like `"IV"` — how should I handle that? I realized I needed to check if the **next** symbol is greater than the **current** one. If so, it means I should subtract the current from the next ( `V (5)` - `I (1)`).

However, this approach brought two problems:

1. What happens when I reach the end of the string?
2. How do I distinguish when to **add** the last numeral vs. when to "ignore" it (because it was already used in a subtraction)?

By "ignore," I mean that in cases like `"IV"`, the subtraction already occurred in the first iteration, so I shouldn't do anything more in the second. But in `"III"`, I should continue adding every symbol.

To solve this, I used the following approach to safely check the next value without going out of bounds:

```python
next_value = Roman_dict[s[i+1]] if i < length_input - 1 else 0
```

This returns `0` if `i` is at the last character, avoiding an index error.

But this alone wasn’t enough. In the case of `"IV"`, when the loop reaches `'V'`, `next_value` is 0, so it would fall into the `else` case and **add** the value again, giving an incorrect result of 9.

So I realized I needed better control over the index. That’s when I switched to using a `while` loop and, crucially, when a subtraction happens, I **skip two characters**.

Let’s look at `"LIX"` (which is 59):

- First iteration: `i = 0`, we check `'L' (50)` and `'I' (1)`. Since 50 >= 1, we add 50 and `i += 1`.
- Second iteration: `i = 1`, we check `'I' (1)` and `'X' (10)`. Since 1 < 10, we add `10 - 1 = 9` and `i += 2`.
- `i = 3`, which exits the loop correctly.

This approach solves both problems: it prevents index errors and avoids double-counting characters.

---



