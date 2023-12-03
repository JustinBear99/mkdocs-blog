---
date:
    created: 2023-12-02
    updated: 2023-12-02

description: >
    Solution for Leet Code 1266. Minimum Time Visiting All Points

tags:
    - LeetCode

comments: true
---
# 1266. Minimum Time Visiting All Points

## Description

Find distance sum for given path. Still an easy problem.. so just code.

## Code

```python
class Solution:
    def minTimeToVisitAllPoints(self, points: List[List[int]]) -> int:
        ans = 0
        for i in range(1, len(points)):
            pre = points[i - 1]
            cur = points[i]

            x_diff, y_diff = abs(pre[0] - cur[0]), abs(pre[1] - cur[1])
            ans += max(x_diff, y_diff)
        return ans
```