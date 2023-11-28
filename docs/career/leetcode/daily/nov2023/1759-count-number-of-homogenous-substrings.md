---
date:
    created: 2023-11-09
    updated: 2023-11-28

description: >
	Solution for Leet Code 1759. Count Number of Homogenous Substrings

tags:
    - LeetCode

comments: true
---
# 1759. Count Number of Homogenous Substrings

## Description

Count the number of substrings that have the same character (homogeneous), including duplicates and the substrings must be contiguous.

## Intuition

The number of homogenous substring of `n` characters is 1+2+...+n. So we can calculate how many of substrings that have length of `n` and sum them up with the equation.

## Code

```python
class Solution:
    def countHomogenous(self, s: str) -> int:
        # the equation for 1+2+...+n
        def countByLength(l):
            return sum(range(1, l + 1, 1))

        i, j = 0, 0
        d = {}
        # loop over the given string and use a map to store how many substrings that have length = 1 or 2 or ...
        while j < len(s):
            if s[j] == s[i]:
                j += 1
            else:
                d[j - i] = d.get(j - i, 0) + 1
                i = j
        d[j - i] = d.get(j - i, 0) + 1
        ans = 0
        for k, v in d.items():
            ans += v * countByLength(k)
        return ans % (10 ** 9 + 7)
```