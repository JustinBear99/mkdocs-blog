---
date:
    created: 2023-12-07
    updated: 2023-12-07

description: >
    Solution for Leet Code 1903. Largest Odd Number in String

tags:
    - LeetCode

comments: true
---
# 1903. Largest Odd Number in String

## Description

Given a number in `str` and we are asked to find the substring of it that has the largest odd number.

## Intuition

To determine if a number is odd, we only need to check the remain of the last digit. Therefore, we can find the substring by checking the last digit of `num`.

## Code

```python
class Solution:
    def largestOddNumber(self, num: str) -> str:
        last_index = len(num)
        for i in range(len(num) - 1, -1, -1):
            if int(num[i]) % 2 == 1:
                break
            last_index = i
        return num[:last_index]
```