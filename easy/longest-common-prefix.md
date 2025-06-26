# Longest Common Prefix #4

 **Link to the problem:** [Longest Common  Prefix- LeetCode](https://leetcode.com/problems/longest-common-prefix/)

## Problem Summary

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

### Example 1:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

### Example 2:
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

### Constraints:
- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters.

---

## Python Solution

```python
def longestCommonPrefix(self, strs: List[str]) -> str:
    shortest_word = min(strs, key=len)
    strs.remove(shortest_word)
    result = ""
    for i in range(len(shortest_word)):
        if all(word[i] == shortest_word[i] for word in strs):
            result += shortest_word[i]
        else:
            break
    return result
```

---

## My Thought Process

First, I extract the shortest word from the list, because if there is a common prefix, it cannot be longer than that word.  
Then, I remove that word from the original list to avoid comparing it against itself.

The goal is to compare whether the first character of every word matches the first character of the shortest word.  
If so, we store that letter. I used a very clean way to do this with:

```python
if all(palabra[i] == Min_word[i] for palabra in strs):
    resultado += Min_word[i]
```

Here’s what that line does:

- At each step of the loop, it compares the character at position `i` of `Min_word` with the character at the same position in every other word.
- If all the words share that character at the same position, it is added to the common prefix (`resultado`).
- As soon as one word does not match, the loop breaks.
- The use of `all()` and a generator expression allows for an elegant and efficient way to verify prefix consistency across all words.

---

## Alternative Elegant Solution

Here is another elegant solution I found, which I found very interesting and worth remembering:

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        prefix = ''

        for chars in zip(*strs):
            if len(set(chars)) == 1:
                prefix += chars[0]
            else:
                break
        return prefix
```

### Explanation

- The `zip(*strs)` function transposes the list of strings, grouping together the characters at the same positions across all strings.
- For example, given `["flower", "flow", "flight"]`, `zip(*strs)` will produce:
  - `('f', 'f', 'f')`
  - `('l', 'l', 'l')`
  - `('o', 'o', 'i')`
  - This is perfect because `zip` automatically stops at the shortest word, just as if we had used `min(strs, key=len)` to limit the comparison range.
- At each iteration, the code checks whether all characters in the tuple are the same using `len(set(chars)) == 1`.
- If they are, it adds that character to the prefix.
- As soon as a mismatch is found (like `'o', 'o', 'i'`), the loop breaks.
