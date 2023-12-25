---
date:
    created: 2023-12-25
    updated: 2023-12-25

description: >
    Solution for Leet Code 91. Decode Ways

tags:
    - LeetCode

comments: true
---
# 91. Decode Ways

## Description

Merry Christmas!

Find the combinations that a string `s` of numbers can transform to letters. `1` represents for `A` and `26` for `Z`. Note that `0` is not allowed to be the first digit.

## Intuition

DP `s` for first one or two letter and plus `numDecodings()` for rest.
- Watch out for edge cases like empty string and `0` started string.
- Handle string starts with `1` and `2` specifically because only string starts with these two can take off two chars at a time.
- Otherwise, take a char for DP.

## Code

```python
from functools import lru_cache

class Solution:
    @lru_cache() # cache the result
    def numDecodings(self, s: str) -> int:
        # edge cases: `0`-start string can never form a valid combination
        if s.startswith('0'):
            return 0
        # last char
        elif len(s) <= 1:
            return 1
        num = 0
        # we can take two chars at a time for string starts with *1* like *11*, *13*.
        if s.startswith('1'):
            num += self.numDecodings(s[2:])
        # we can also take two chars for string starts with *2* as long as the next char is still valid.
        elif s.startswith('2') and s[1] in ['0', '1', '2', '3', '4', '5', '6']:
            num += self.numDecodings(s[2:])
        # select one char by default
        return num + self.numDecodings(s[1:])
```