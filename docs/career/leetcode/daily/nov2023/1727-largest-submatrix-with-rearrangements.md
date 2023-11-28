---
date:
    created: 2023-11-27
    updated: 2023-11-28

description: >
    Solution for Leet Code 1727. Largest Submatrix With Rearrangements

tags:
    - LeetCode

comments: true
---
# 1727. Largest Submatrix With Rearrangements

## Description

We are asked to find the largest matrix such that the values of this matrix are all `1`. We can switch the column of the given matrix but not for the row.

## Intuition

Actually, I follow the [idea](https://leetcode.com/problems/largest-submatrix-with-rearrangements/solutions/4330528/beats-100-simple-dynamic-programming-approach-no-extra-space/?envType=daily-question&envId=2023-11-26) from *jailwalankit* (please upvote his solution) since I'm not good at this kind of spatial question and didn't figure out in 5 mins.

Anyway, the idea is to find *the number of consecutive `1`s looking up from a cell* so we don't bother to look at a segment to matrix to know the maximum possible submatrix *height*. The second step is to sort the row to find the *width*.

## Code

```python
class Solution:
    def largestSubmatrix(self, matrix: List[List[int]]) -> int:
        m, n = len(matrix), len(matrix[0])

        for i in range(1, m):
            for j in range(n):
                if matrix[i][j] == 1:
                    matrix[i][j] += matrix[i - 1][j]
        ans = 0
        for i in range(m):
            matrix[i].sort(reverse=True)
            for j in range(n):
                ans = max(ans, matrix[i][j] * (j + 1))
        return ans
```