---
date:
  created: 2023-10-29
  updated: 2023-11-28

description: >
  Solution for Leet Code 458. Poor Pigs

tags:
  - LeetCode

comments: true
---

# 458. Poor Pigs

## Description

2023.10.29

At first glance, this problem looks like to test the math/logic, but I couldn't figure it out in 10 minutes.

Here's the solution I found helpful:
1. logirithm: 
    1. https://leetcode.com/problems/poor-pigs/solutions/4220289/c-log2-1-line/
    2. https://leetcode.com/problems/poor-pigs/solutions/2387610/python-detailed-explanation-faster-than-98-easily-understood-simple-math/ 
2. stepby step concept: 
    1. https://leetcode.com/problems/poor-pigs/solutions/94266/another-explanation-and-solution/?envType=daily-question&envId=2023-10-29

## Code

```python
## same as the second one
class Solution:
    def poorPigs(self, buckets: int, minutesToDie: int, minutesToTest: int) -> int:
        pigs = 0
        while (minutesToTest / minutesToDie + 1) ** pigs < buckets:
            pigs += 1
        return pigs
```