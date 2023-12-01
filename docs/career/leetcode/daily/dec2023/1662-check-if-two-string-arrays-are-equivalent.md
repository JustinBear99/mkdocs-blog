---
date:
    created: 2023-11-13
    updated: 2023-11-28

description: >
    Solution for Leet Code 1662. Check If Two String Arrays are Equivalent

tags:
    - LeetCode

comments: true
---
# 1662. Check If Two String Arrays are Equivalent

## Description

Determine if two list of strings are the same after concatenated.

## Code

Since it's an easy problem, do it easily.

```python
class Solution:
    def arrayStringsAreEqual(self, word1: List[str], word2: List[str]) -> bool:
        return "".join(word1) == "".join(word2)
```