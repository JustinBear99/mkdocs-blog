---
date:
    created: 2023-12-10
    updated: 2023-12-10

description: >
    Solution for Leet Code 867. Transpose Matrix

tags:
    - LeetCode

comments: true
---
# 867. Transpose Matrix

## Description

Transpose 2d matrix. (10 *easy* problems streak... 😑)

## Code

```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        m, n = len(matrix), len(matrix[0])
        return [[ matrix[j][i] for j in range(m)] for i in range(n)]
```