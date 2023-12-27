---
date:
    created: 2023-12-27
    updated: 2023-12-27

description: >
    Solution for Leet Code 1155. Number of Dice Rolls With Target Sum

tags:
    - LeetCode

comments: true
---
# 1155. Number of Dice Rolls With Target Sum

## Description

Similar to the problem of 25 Dec, iterate to find the combinations and use cache to prevent unnecessary calculation.

## Code

```python
class Solution:
    def numRollsToTarget(self, n: int, k: int, target: int) -> int:
        if n > target:
            return 0
        self.MOD = 10 ** 9 + 7
        self.cache = [[None for _ in range(1001)] for _ in range(31)]
        return self.inner(n, k-1, target-n)

    def inner(self, n, k, target):
        if n * k < target:
            return 0
        if n == 1:
            return 1 if k >= target else 0
        if self.cache[n][target] != None:
            return self.cache[n][target]
        ret = 0
        for num in range(min(k+1, target+1)):
            ret += self.inner(n - 1, k, target - num)
            ret %= self.MOD
        self.cache[n][target] = ret
        return ret

```