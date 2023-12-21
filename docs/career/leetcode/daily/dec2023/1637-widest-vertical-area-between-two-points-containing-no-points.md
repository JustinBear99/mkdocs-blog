---
date:
    created: 2023-12-21
    updated: 2023-12-21

description: >
    Solution for Leet Code 1637. Widest Vertical Area Between Two Points Containing No Points

tags:
    - LeetCode

comments: true
---
# 1637. Widest Vertical Area Between Two Points Containing No Points

## Description

Sort by x axis and find the largest x difference between each two points.

## Code

```python
class Solution:
    def maxWidthOfVerticalArea(self, points: List[List[int]]) -> int:
        ans = 0
        points.sort()
        for i in range(1, len(points)):
            ans = max(ans, points[i][0] - points[i-1][0])
        return ans
```