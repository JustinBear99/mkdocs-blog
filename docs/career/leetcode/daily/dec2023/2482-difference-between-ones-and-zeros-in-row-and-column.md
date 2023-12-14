---
date:
    created: 2023-12-14
    updated: 2023-12-14

description: >
    Solution for Leet Code 2482. Difference Between Ones and Zeros in Row and Column

tags:
    - LeetCode

comments: true
---
# 2482. Difference Between Ones and Zeros in Row and Column

## Description

Pretty similar to yesterday's problem, just do row col count from every point.

## Code

```python
class Solution:
    def onesMinusZeros(self, grid: List[List[int]]) -> List[List[int]]:
        m, n = len(grid), len(grid[0])
        ones_row, ones_col = [0] * m, [0] * n
        diff = [[0 for _ in range(n)] for _ in range(m)]
        for i in range(m):
            for j in range(n):
                ones_row[i] += grid[i][j]
                ones_col[j] += grid[i][j]
        for i in range(m):
            for j in range(n):
                d = 2 * (ones_row[i] + ones_col[j]) - (m + n)
                diff[i][j] = d
        return diff
```