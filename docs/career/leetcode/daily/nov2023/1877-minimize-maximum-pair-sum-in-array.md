---
date:
    created: 2023-11-17
    updated: 2023-11-28

description: >
	Solution for Leet Code 1877. Minimize Maximum Pair Sum in Array

tags:
    - LeetCode

comments: true
---
# 1877. Minimize Maximum Pair Sum in Array

## Description

Find the maximum sum of pair in `nums` from `len(nums) / 2` pairs formed by `nums` and no duplicates. And then, minimized the maximum value.

## Intuition

To make the pair sum minimized, we can greedyly sort `nums` and pair from the smallest and the largest values.

Proof:

Let nums = [a<sub>0</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>, a<sub>n</sub>] and a<sub>0</sub> <= a<sub>1</sub> <= ... <= a<sub>n-1</sub> <= a<sub>n</sub>.
Assume there exists another way (a<sub>i</sub>, a<sub>n-i+j</sub>) to form the pairs that has maximum pair sum smaller than forming by (a<sub>i</sub>, a<sub>n-i</sub>).
In other words, max of (a<sub>i</sub> + a<sub>n-i+j</sub>) pairs should always be less than or equal to max of (a<sub>i</sub> + a<sub>n-i</sub>) pairs which implies that we can make the pair sum smaller by shuffling at least two pairs.

Let's say the shuffled pairs originally have sum of `u` and `v` and the sums become `u + x` and `v - x` where x >=0. Since max(`u + x`, `v - x`) must >= max(`u`, `v`) violates previous assumption, the maximum value of pair sum forming by (ai, an-i) must be minimized.

## Code

```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        nums.sort()
        n = len(nums)
        ans = 0
        for i in range(int(n / 2)):
            s = nums[i] + nums[n - 1 - i]
            if s > ans:
                ans = s
        return ans
```