---
date:
    created: 2023-12-16
    updated: 2023-12-16

description: >
    Solution for Leet Code 242. Valid Anagram

tags:
    - LeetCode

comments: true
---
# 242. Valid Anagram

## Description

Count character appearance for two strings.

## Code

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        base = ord('a')
        count = [0] * 26
        for c in s:
            count[ord(c) - base] += 1
        for c in t:
            count[ord(c) - base] -= 1
        for c in count:
            if c != 0:
                return False
        return True
```