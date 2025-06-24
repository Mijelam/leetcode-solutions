#  Two Sum – LeetCode #1
**Link to the problem:** [Two Sum – LeetCode](https://leetcode.com/problems/two-sum/)  
---

##  Problem Summary

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the target.  
You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example 1:**  
Input: `nums = [2,7,11,15]`, `target = 9`  
Output: `[0,1]`

---

##  Python Solution
```python

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for index, value in enumerate(nums):
            complement = target - value
            if complement in nums and nums.index(complement) != index:
                return [index, nums.index(complement)]
```
##  My Thought Process

Since the input is a list of integers and I'm required to return the **indices** of two numbers that add up to a target, the first thing that came to mind was using `enumerate()` — it lets me loop through each value while keeping track of its position.

Then I asked myself:  
> “How can I know if there's another number in the list that pairs with the current one to reach the target?”

The answer was to compute the **complement** by doing `target - current_value`.

For each element:
- I check if that complement exists in the list.
- I make sure its index is **not equal** to the current one.  
  This is crucial — without that condition, I could return the same index twice, which would break the problem's constraint. For example:  
  If `nums = [3, 5, 3]` and `target = 6`, I must not return `[0, 0]`.

Finally, I return the two indices using the current index from `enumerate()` and the index of the complement using `nums.index()`.

This approach works well for short inputs and is easy to understand. However, it’s less efficient than the more common solution that uses a **dictionary** to store previously seen numbers as keys and their indices as values. 
Still, I chose to implement this one because I found it intuitive and wanted to explore a different way to solve the problem.

