---
date:
  created: 2023-11-27
  updated: 2023-11-27

tags:
    - LeetCode

comments: true
---
# 935. Knight Dialer

## Description

We are requested to find the number of combination for phone number of length `n`. The limitation is that the consecutive digits follow the movement of knight in chess.

## Intuition

Since the possible paths from number `i` to `j` are fixed, we can construct the transition matrix for calculating the number of path ending what digit.

In addition, since we will multiply the same matrix multiple times, we can actually benefit from the [attibute of matrix](https://leetcode.com/problems/knight-dialer/solutions/189252/o-logn/?envType=daily-question&envId=2023-11-27) (linear algebra stuff that I didn't think of it while solving this problem 😂). The time complexity becomes `O(logn)`.

## Code

```python
class Solution:
    def knightDialer(self, n: int) -> int:
        def round(count):
            return [
                count[4] + count[6], # 4 and 6 can goes to 0 or say 0 came from 4 or 6
                count[6] + count[8],
                count[7] + count[9],
                count[4] + count[8],
                count[0] + count[3] + count[9],
                0,
                count[0] + count[1] + count[7],
                count[2] + count[6],
                count[1] + count[3],
                count[2] + count[4]
            ]
        
        count = [1 for i in range(10)]
        for i in range(n - 1):
            count = round(count)
        return sum(count) % (10 ** 9 + 7)
```