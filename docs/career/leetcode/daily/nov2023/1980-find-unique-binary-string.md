---
date:
  created: 2023-11-16
  updated: 2023-11-16

tags:
    - LeetCode

comments: true
---
# 1980. Find Unique Binary String

## Description

The [problem](https://leetcode.com/problems/find-unique-binary-string/description/?envType=daily-question&envId=2023-11-16) ask for one of the binary string of length `n` that doesn't exist in the given `nums`.

## Intuition

Since the length of `n` is given, one may list all possible combinations and remove by `nums`. However, the time complexity would be O(len(nums) * 2 ^ n).

As we only requested to return one of the valid answers, we can think about what makes two binary different? The answer is ... at least one digit holds different value! Hence, we just need to create a binary string that have all `n` digits each being different with one of the number in `nums`

## Code

```python
class Solution:
    def findDifferentBinaryString(self, nums: List[str]) -> str:
        ans = []
        for i in range(len(nums)):
            ans.append("1" if nums[i][i] == "0" else "0")
        return "".join(ans)
```