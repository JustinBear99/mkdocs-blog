---
date:
    created: 2023-12-19
    updated: 2023-12-19

description: >
    Solution for Leet Code 661. Image Smoother

tags:
    - LeetCode

comments: true
---
# 661. Image Smoother

## Description

Just loop through all indices

## Code

```python
class Solution:
    def imageSmoother(self, img: List[List[int]]) -> List[List[int]]:
        m, n = len(img), len(img[0])
        ret = [[0 for _ in range(n)] for _ in range(m)]
        for i in range(m):
            for j in range(n):
                l = []
                for x, y in ((i-1, j-1), (i-1,j), (i-1, j+1), (i, j-1), (i,j), (i,j+1), (i+1, j-1), (i+1, j), (i+1,j+1)):
                    if 0 <= x < m and 0 <= y < n:
                        l.append(img[x][y])
                ret[i][j] = sum(l) // len(l)
        return ret
```