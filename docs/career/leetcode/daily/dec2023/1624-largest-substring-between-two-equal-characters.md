---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 1624. Largest Substring Between Two Equal Characters

tags:
    - LeetCode

comments: true
---
# 1624. Largest Substring Between Two Equal Characters

## Description

Record the first index of characters showing up

## Code

```python
class Solution:
    def maxLengthBetweenEqualCharacters(self, s: str) -> int:
        ans = -1
        base = ord('a')
        table = {i: -1 for i in range(26)}
        for i in range(len(s)):
            key = ord(s[i]) - base
            if table[key] == -1:
                table[key] = i
            else:
                ans = max(ans, i - table[key] - 1)
        return ans
```