---
date:
    created: 2023-12-15
    updated: 2023-12-15

description: >
    Solution for Leet Code 1436. Destination City

tags:
    - LeetCode

comments: true
---
# 1436. Destination City

## Description

Given directed `path` from `path[0]` to `path[1]`. Find the `path[1]` that never appear in the first element.

## Code

```python
class Solution:
    def destCity(self, paths: List[List[str]]) -> str:
        table = {} # record appearance
        for f, t in paths: # for from, to in paths
            if f not in table:
                table[f] = 0
            if t not in table:
                table[t] = 0
            table[f] += 1
        for k, v in table.items():
            if v == 0:
                return k
        return ""
```