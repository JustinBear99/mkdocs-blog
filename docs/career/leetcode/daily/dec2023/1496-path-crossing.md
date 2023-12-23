---
date:
    created: 2023-12-23
    updated: 2023-12-23

description: >
    Solution for Leet Code 1422. Maximum Score After Splitting a String

tags:
    - LeetCode

comments: true
---
# 1496. Path Crossing

## Description

Use set to remember where we have been before.

## Code

```python
class Solution:
    def isPathCrossing(self, path: str) -> bool:
        direction = {'N': (0, 1), 'S': (0, -1), 'E': (1, 0), 'W': (-1, 0)}
        point = [0, 0]
        s = set()
        s.add(tuple(point))
        for p in path:
            d = direction[p]
            point[0] = point[0] + d[0]
            point[1] = point[1] + d[1]
            t = tuple(point)
            if t in s:
                return True
            s.add(t)
        return False
```