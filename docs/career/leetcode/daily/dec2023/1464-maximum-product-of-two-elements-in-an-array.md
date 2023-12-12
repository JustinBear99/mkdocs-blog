---
date:
    created: 2023-12-12
    updated: 2023-12-12

description: >
    Solution for Leet Code 1464. Maximum Product of Two Elements in an Array

tags:
    - LeetCode

comments: true
---
# 1464. Maximum Product of Two Elements in an Array

## Description

Find the largest two numbers.

## Code

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        i, j = 0, 0
        for num in nums:
            if num > i or num > j:
                if i > j:
                    j = num
                else:
                    i = num
        return (i - 1) * (j - 1)
```