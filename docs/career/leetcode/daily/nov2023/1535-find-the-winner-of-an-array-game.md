---
date:
    created: 2023-11-05
    updated: 2023-11-28

description: >
    Solution for Leet Code 1535. Find the Winner of an Array Game

tags:
    - LeetCode

comments: true
---

# 1535. Find the Winner of an Array Game

## Description

We wan to find the first one that meet a win streak of `k` from the given `arr` with the losed one added back to `arr`. Therefore, `k` can be larger than the length of `arr`

## Intuition

Follow the rules from the problem to use queue and while loop for comparision since the problem promise that the answer exist.

## Code

```python
class Solution:
    def getWinner(self, arr: List[int], k: int) -> int:
        # Only the largest one can have win streak more or equal to the number of whole group.
        if k >= len(arr):
            return max(arr)

        streak = 0
        q = collections.deque(arr)
        defender = q.popleft()

        while streak < k:
            challenger = q.popleft()
            if defender > challenger:
                q.append(challenger)
                streak += 1
            else:
                q.append(defender)
                defender = challenger
                streak = 1
        return defender
```