---
date:
    created: 2023-12-06
    updated: 2023-12-06

description: >
    Solution for Leet Code 1716. Calculate Money in Leetcode Bank

tags:
    - LeetCode

comments: true
---
# 1716. Calculate Money in Leetcode Bank

## Description

Sum the array of length `n` with given array formation rules.

## Code

```python
class Solution:
    def totalMoney(self, n: int) -> int:
        ans = 0
        week, weeks, days = 0, n // 7, n % 7
        for week in range(1, weeks + 1):
            ans += 28 + 7 * (week - 1)
        for day in range(1, days + 1):
            ans += day + week
        return ans
```