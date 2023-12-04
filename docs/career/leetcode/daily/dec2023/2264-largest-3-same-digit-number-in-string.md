---
date:
    created: 2023-12-04
    updated: 2023-12-04

description: >
    Solution for Leet Code 2264. Largest 3-Same-Digit Number in String

tags:
    - LeetCode

comments: true
---
# 2264. Largest 3-Same-Digit Number in String

## Description

Find the largest consecutive substring of three same characters. (4 consecitive `easy` problems, *ResidentSleeper*)

## Code

```python
class Solution:
    def largestGoodInteger(self, num: str) -> str:
        cur = None
        for i in range(2, len(num)):
            if num[i] == num[i - 1] and num[i] == num[i - 2]:
                if not cur or int(num[i]) > int(cur):
                    cur = num[i]
        if not cur:
            return ""
        return cur + cur + cur
```