---
date:
  created: 2023-11-21
  updated: 2023-11-21

tags:
    - LeetCode

comments: true
---
# 2391. Minimum Amount of Time to Collect Garbage

## Description

Since the trucks start from index 0 and must travel houses one by one, we only need to find the last index of every kind of garbage appearing. We can use prefix sum to decrease the summing time required, however, it doesn't affect time complexity much.

## Code

```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        table = {"M": [0, 0], "P": [0, 0], "G": [0, 0]} # [count, last seen index] for M P G
        for i in range(len(garbage)):
            for g in garbage[i]:
                table[g][0] += 1
                table[g][1] = i
        ans = 0
        for c, i in table.values():
            ans += c
            ans += sum(travel[:i]) if i > 0 else 0
        return ans
```