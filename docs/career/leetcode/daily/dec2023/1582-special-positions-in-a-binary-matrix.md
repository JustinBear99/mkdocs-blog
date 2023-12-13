---
date:
    created: 2023-12-13
    updated: 2023-12-13

description: >
    Solution for Leet Code 1582. Special Positions in a Binary Matrix

tags:
    - LeetCode

comments: true
---
# 1582. Special Positions in a Binary Matrix

## Description

Find the position that only the element is one for the row and col it belongs to. (Feel this problem a bit like medium question. 😅)

## Intuition

1. Loop through the matrix to count the number of 1's for rows and columns and record its position for later use.
2. For all positions that is one, if it's row count and column count are also one, it is quaranteed that that position is the only one. 

## Code

```python
class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        m, n = len(mat), len(mat[0])
        row, col = [0] * m, [0] * n
        candidate = []
        for i in range(m):
            for j in range(n):
                if mat[i][j] == 1:
                    row[i] += 1
                    col[j] += 1
                    candidate.append((i, j))
        ans = 0
        for i, j in candidate:
            if row[i] == 1 and col[j] == 1:
                ans += 1
        return ans
```