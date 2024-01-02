---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 455. Assign Cookies

tags:
    - LeetCode

comments: true
---
# 455. Assign Cookies

## Description

Find the number of `g`'s elements that are less or equals by `s`'s elements. Each can only be used once.

## Code

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        if not g or not s:
            return 0
        g.sort()
        s.sort()
        i, j = 0, 0
        while i < len(g) and j < len(s):
            if s[j] >= g[i]:
                i += 1
            j += 1
        return i
```