---
date:
  created: 2023-11-25
  updated: 2023-11-25

tags:
    - LeetCode

comments: true
---
# 1685. Sum of Absolute Differences in a Sorted Array

## Description

We are asked to find the sum of absolute difference for every element with respect to other elements in a [sorted array](https://leetcode.com/problems/sum-of-absolute-differences-in-a-sorted-array/description/?envType=daily-question&envId=2023-11-25). 

## Intuition

As the array, `nums`, is sorted, we can get rid of `abs()` operation to calculate difference sum. In other words, difference sum of index `i` equals to `nums[i] * (i + 1) - sum(nums[:i])` plus `sum(nums[i:]) - nums[i] * (n - i - 1)`. Also, we can use prefix sum to prevent repetitive sum operation.

## Code

```python
class Solution:
    def getSumAbsoluteDifferences(self, nums: List[int]) -> List[int]:
        n = len(nums)
        p_sum = [0] * n
        for i in range(n):
            p_sum[i] = p_sum[i - 1] + nums[i]

        ans = []
        for i in range(n):
            pre = p_sum[i] # includes nums[i]
            post = p_sum[-1] - p_sum[i]
            s_pre = nums[i] * (i + 1) - pre 
            s_post = post - nums[i] * (n - i - 1)
            ans.append(s_pre + s_post)
        return ans
```