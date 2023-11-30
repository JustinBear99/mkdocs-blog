---
date:
    created: 2023-11-29
    updated: 2023-11-30

description: >
    Solution for Leet Code 191. Number of 1 Bits

tags:
    - LeetCode

comments: true
---
# 191. Number of 1 Bits

## Description

Find the number of bit `1` in the binary representation of given integer.

## Code

```python
# Divide and remain
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans = 0
        while n > 0:
            if n % 2 == 1:
                ans += 1
            n = n // 2
        return ans

# bit manipulation
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans = 0
        while n:
            n &= n - 1
            ans += 1
        return ans
```