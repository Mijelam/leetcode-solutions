# Remove Element - LeetCode #7

**Link to the problem :** [Remove Element -  LeetCode](https://leetcode.com/problems/remove-element)

## Problem Summary

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in-place. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

It doesn't matter what you leave beyond the returned length.

### Example 1:
```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
```
### Example 2:
```
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
```

## Python Solution

```python
def removeElement(self, nums: List[int], val: int) -> int:
    k = 0
    for i in range(len(nums)):
        if nums[i] != val:
            nums[k] = nums[i]
            k += 1
    return k
```

## My Thought Process

This problem is very easy to solve if you've previously done the "Remove Duplicates from Sorted Array" challenge, since both are quite similar in structure and logic. The idea is to iterate over the array and selectively overwrite values to keep only the ones that are allowed.

## Explanation

We use a variable `k` to track the position where we want to store the next non-`val` element. As we iterate over the array, if the current element is different from `val`, we move it to the index `k` and increment `k`. At the end of the loop, the first `k` elements in the array are the elements that are not equal to `val`. The function then returns `k` as the new length of the array.
