---
date:
  created: 2023-11-23
  updated: 2023-11-23

tags:
    - LeetCode

comments: true
---
# 1630. Arithmetic Subarrays

## Description

Given integer list `nums`, we are asked to find if the subarray from index `i` to `j` is arithmetic or not. See the definition in the [problem](https://leetcode.com/problems/arithmetic-subarrays/?envType=daily-question&envId=2023-11-23).

## Intuition

After seeing the problem, my first idea is to use dynamic programming or sliding window stuff to iterate combination. However, soon I realized that the result of subarray `(i, j)` is either independent to subarray `(i, j + 1)` or `(i, j - 1)`, etc. We actually can't reuse the result for optimizing our alogorithm.

The brute force way is to determine `m` subarray independenty with sorting. The time complexity is expected to be `O(m * nlog(n))` where `n` is the average length of subarray.

To decrease the time consumed (use methods of time complexity less than `O(nlogn)` only), we should rethink about the criteria about arithmaic subarray. If an array is arithmatic, we can confirm that the difference of adjacent elements are the same and equals to `(max - min) / (size - 1)`. For example, if there is an array `[40, 20, 60, 30, 50, 10]`. After looping and finding that the min=`10` and max=`60`, it is expected that elements `20`, `30`, `40` and `50` should be at index `1`, `2`, `3`and `4`. If we can't find the index exists or the indexes not filled, then the array is not arithmatic. The overall time complexity will be `O(m*n)`.

## Code

```python
# First intuition, easy and takes time (not bad actually).
class Solution:
    def checkArithmeticSubarrays(self, nums: List[int], l: List[int], r: List[int]) -> List[bool]:
        def isArithmetic(nums):
            nums.sort()
            for i in range(2, len(nums)):
                if nums[i] - nums[i - 1] != nums[i - 1] - nums[i - 2]:
                    return False
            return True

        ans = []
        for i in range(len(l)):
            sub = nums[l[i]: r[i] + 1]
            ans.append(isArithmetic(sub))
        return ans

# Second intuition but fail at edge cases. Don't want to fix this, just a reference. lol
class Solution:
    def checkArithmeticSubarrays(self, nums: List[int], l: List[int], r: List[int]) -> List[bool]:
        def isArithmetic(nums):
            n = len(nums)
            ret = [None] * n
            mini, maxi = float("inf"), float("-inf")
            for num in nums:
                if num < mini:
                    mini = num
                elif num > maxi:
                    maxi = num
            diff = (maxi - mini) / (n - 1)
            if not diff.is_integer():
                return False
            diff = int(diff)
            if diff == 0:
                for num in nums:
                    if num != mini:
                        return False
            else:
                for num in nums:
                    index = (num - mini) / diff
                    if not index.is_integer():
                        return False
                    index = int(index)
                    if index < n:
                        ret[index] = True
            return not (None in ret)

        ans = []
        for i in range(len(l)):
            sub = nums[l[i]: r[i] + 1]
            ans.append(isArithmetic(sub))
        return ans
```