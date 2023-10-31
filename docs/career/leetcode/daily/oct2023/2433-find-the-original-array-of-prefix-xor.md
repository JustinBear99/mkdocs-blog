---
date:
  created: 2023-10-31
  updated: 2023-10-31

tags:
    - LeetCode

comments: true
---
# 2433. Find The Original Array of Prefix Xor

## Description

Pretty straight forward [problem](https://leetcode.com/problems/find-the-original-array-of-prefix-xor/description/?envType=daily-question&envId=2023-10-31), [XOR cipher](https://en.wikipedia.org/wiki/XOR_cipher). To decrypt is to do xor again.

## Code

```python
class Solution:
    def findArray(self, pref: List[int]) -> List[int]:
        ans = [pref[0]]
        for i in range(1, len(pref)):
            ans.append(pref[i] ^ pref[i - 1])
        return ans
```