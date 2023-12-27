---
date:
    created: 2023-12-27
    updated: 2023-12-27

description: >
    Solution for Leet Code 1578. Minimum Time to Make Rope Colorful

tags:
    - LeetCode

comments: true
---
# 1578. Minimum Time to Make Rope Colorful

## Description

Use sliding window to find the consecutive ballons to determine the time for removal.

## Code

```python
class Solution:
    def minCost(self, colors: str, neededTime: List[int]) -> int:
        def calculate(l, r):
            times = neededTime[l:r]
            return sum(times) - max(times)
        
        ans = 0
        l, r = 0, 0
        while l < len(colors) and r < len(colors):
            if colors[l] == colors[r]:
                r += 1
            else:
                ans += calculate(l, r)
                l = r
        ans += calculate(l, r)
        return ans
    
```