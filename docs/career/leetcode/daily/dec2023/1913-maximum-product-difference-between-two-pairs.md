---
date:
    created: 2023-12-17
    updated: 2023-12-17

description: >
    Solution for Leet Code 1913. Maximum Product Difference Between Two Pairs

tags:
    - LeetCode

comments: true
---
# 1913. Maximum Product Difference Between Two Pairs

## Description

Find the highest two and lowest two elements.

## Code

```python
class Solution:
    def maxProductDifference(self, nums: List[int]) -> int:
        # left, right. just naming. lol
        l1, l2, r1, r2 = -float("inf"), -float("inf"), float("inf"), float("inf")
        for num in nums:
            if num > l2:
                if num > l1:
                    l2 = l1
                    l1 = num
                else:
                    l2 = num
            if num < r2:
                if num < r1:
                    r2 = r1
                    r1 = num
                else:
                    r2 = num
        return l1 * l2 - r1 * r2
```