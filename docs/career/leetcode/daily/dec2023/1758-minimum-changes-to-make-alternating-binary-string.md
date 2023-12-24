---
date:
    created: 2023-12-24
    updated: 2023-12-24

description: >
    Solution for Leet Code 1758. Minimum Changes To Make Alternating Binary String

tags:
    - LeetCode

comments: true
---
# 1758. Minimum Changes To Make Alternating Binary String

## Description

Find the minimum steps to make given string become the same as the target.

## Code

```python
class Solution:
    def minOperations(self, s: str) -> int:
        choices = ['0', '1']
        type_1, type_2 = 0, 0
        for i in range(len(s)):
            remain = i % 2
            if s[i] == choices[remain]:
                type_1 += 1
            else:
                type_2 += 1
        return min(type_1, type_2)
```