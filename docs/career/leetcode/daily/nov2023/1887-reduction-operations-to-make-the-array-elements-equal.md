---
date:
    created: 2023-11-19
    updated: 2023-11-28

description: >
    Solution for Leet Code 1887. Reduction Operations to Make the Array Elements Equal

tags:
    - LeetCode

comments: true
---
# 1887. Reduction Operations to Make the Array Elements Equal

## Description

We are asked to decrease all elements in `nums` to the lowest one. However, based on the rules described in the problem, we can only lower the element to the next smaller one and this counts as one operation.

## Intuition

1. Count the numbers of values appeared in `nums` and sort `(value, number)` in descending oeder.
2. For loop the sorted array from large to small and sum up the `value`.
3. Notice that the larger values will be descreased in the next round.

## Code

```python
class Solution:
    def reductionOperations(self, nums: List[int]) -> int:
        count = collections.Counter(nums)
        s = sorted(count.items(), reverse=True)
        ans = 0
        c = 0
        for i in range(len(s) - 1):
            c += s[i][1]
            ans += c
        return ans
```