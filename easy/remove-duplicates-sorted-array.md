# Remove Duplicates from Sorted Array -LeetCode #6

**Link to the problem:** [Remove Duplicates from Sorted Array – LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array)

## Problem Summary

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be kept the same.

Return the number of unique elements `k`, and modify the input array `nums` such that the first `k` elements of `nums` contain the unique elements in order.



### Examples:

**Input:** `nums = [1,1,2]`  
**Output:** `2, nums = [1,2,_]`

**Input:** `nums = [0,0,1,1,1,2,2,3,3,4]`  
**Output:** `5, nums = [0,1,2,3,4,_,_,_,_,_]`

## Python Solution

```python
def removeDuplicates(self, nums: List[int]) -> int:
    k = 1
    for i in range(len(nums) - 1):
        if nums[i] != nums[i + 1]:
            nums[k] = nums[i + 1]
            k += 1
    return k
```

## My Thought Process

The key to this problem is understanding exactly what needs to be done. It might be a bit confusing at first, but I broke it down as follows:

I need to compare each number with the one that comes after it. If they are equal, I do nothing,this means it's a duplicate. But if they are different, I need to keep that new number. The question is: where should I place this new unique number?

This is where the variable `k = 1` becomes important. It has two purposes: it tracks the position where the next unique number should go, and it also ends up counting the number of unique values found.

Why is the loop written like this?
```python
for i in range(len(nums) - 1):
```
Because inside the loop I am accessing `nums[i + 1]`. So by stopping at `len(nums) - 1`, I avoid an index error.

### Example:
Suppose we have the list `[0, 0, 1]`. Initially, `k = 1`. Let's walk through the process:

- Compare first 0 with the second 0 → they're equal, so do nothing.
- Compare second 0 with 1 → they're different, so we take `nums[i + 1]` (which is 1) and assign it to `nums[k]`. Now `nums = [0, 1, 1]` and we increment `k` to 2.

We do this because if we find a new unique value, we want to store it at position `k`. If `k` had started at 0, then the list would have incorrectly become `[1, 0, 1]`, which is not what we want.

## Explanation

This solution uses a simple loop and two pointers. The first pointer `i` goes through the array from start to second-to-last element. The second pointer `k` keeps track of the position where the next unique value should be written.

- Start with `k = 1`, assuming the first element is always unique.
- For each element, compare it with the next one.
- If they're different, it's a new unique value.
- Assign this new value to position `k`, and increment `k`.

After the loop ends, the first `k` elements of the array are the unique ones, and `k` is the count of them.
