---
date:
    created: 2023-12-22
    updated: 2023-12-22

description: >
    Solution for Leet Code 1422. Maximum Score After Splitting a String

tags:
    - LeetCode

comments: true
---
# 1422. Maximum Score After Splitting a String

## Description

Iterate through the string and count number of `0` and `1` for each position

## Code

```python
class Solution:
    def maxScore(self, s: str) -> int:
        num_one = 0
        for c in s:
            if c == "1":
                num_one += 1
        num_zero = 0
        ans = 0
        for i in range(len(s) - 1):
            if s[i] == "1":
                num_one -= 1
            else:
                num_zero += 1
            ans = max(ans, num_one + num_zero)
        return ans
```