---
date:
    created: 2023-12-05
    updated: 2023-12-05

description: >
    Solution for Leet Code 1688. Count of Matches in Tournament

tags:
    - LeetCode

comments: true
---
# 1688. Count of Matches in Tournament

## Description

Find the matches required for `n` teams.

## Code

```python
# based on the logic in description
class Solution:
    def numberOfMatches(self, n: int) -> int:
        ans = 0
        while n > 1:
            ans += n // 2
            if n % 2 == 1:
                n += 1
            n = n // 2
        return ans

# or with observation

class Solution:
    def numberOfMatches(self, n: int) -> int:
        return n - 1
```