---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 1897. Redistribute Characters to Make All Strings Equal

tags:
    - LeetCode

comments: true
---
# 1897. Redistribute Characters to Make All Strings Equal

## Description

Count the appearance of all characters.

## Code

```python
class Solution:
    def makeEqual(self, words: List[str]) -> bool:
        counter = {}
        for word in words:
            for c in word:
                if c not in counter:
                    counter[c] = 0
                counter[c] += 1
        n = len(words)
        for k, v in counter.items():
            if v % n != 0:
                return False
        return True
```