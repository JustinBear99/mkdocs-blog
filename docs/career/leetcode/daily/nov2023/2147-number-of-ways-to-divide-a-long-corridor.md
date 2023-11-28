---
date:
    created: 2023-11-28
    updated: 2023-11-28

description: >
	Solution for Leet Code 2147. Number of Ways to Divide a Long Corridor

tags:
    - LeetCode

comments: true
---
# 2147. Number of Ways to Divide a Long Corridor

## Description

Given a string representing a corridor which contains only seat and plant. We are asked to find the number of combination of dividing them into segments. The segment must contains exactly two seats.

## Intuition

The only limitation is to have each segment containing exactly two seats so the key is to find *how many plants between the segments*. Hence:

1. Find the indexes of seats in the corridor.
2. Check for edge cases of (not enough seats).
3. Count the number of plants between segment and return the production.



## Code

```python
class Solution:
    def numberOfWays(self, corridor: str) -> int:
        s = [i for i in range(len(corridor)) if corridor[i] == "S"]
        if not s or len(s) % 2 != 0:
            return 0
        ans = [1]
        # start from second segment, find the length with last segment
        for i in range(2, len(s), 2):
            ans.append(s[i] - s[i - 1])
        return math.prod(ans) % (10 ** 9 + 7)
```

```
S S P P S P S
0 1 2 3 4 6 7
  ↑     ↑
 i-1    i
```