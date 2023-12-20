---
date:
    created: 2023-12-20
    updated: 2023-12-20

description: >
    Solution for Leet Code 2706. Buy Two Chocolates

tags:
    - LeetCode

comments: true
---
# 2706. Buy Two Chocolates

## Description

Find the lowest two elements

## Code

```python
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        m1, m2 = float("inf"), float("inf")
        for price in prices:
            if price < m2:
                if price < m1:
                    m2 = m1
                    m1 = price
                else:
                    m2 = price
        return money - (m1 + m2) if m1 + m2 <= money else money
```