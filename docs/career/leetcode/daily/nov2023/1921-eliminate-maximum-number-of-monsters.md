---
date:
    created: 2023-11-07
    updated: 2023-11-28

description: >
	Solution for Leet Code 1921. Eliminate Maximum Number of Monsters

tags:
    - LeetCode

comments: true
---
# 1921. Eliminate Maximum Number of Monsters

## Description

In my opinion, the problem is sort of insufficient. For example, it doesn't say when can we eliminate a monster. Do we have to wait for them coming or can we kill one once the weapon is charged. Intuitively, I thought we are staying at **0** waiting for monsters coming but turning out that we can eliminate one once it's charged.

## Code

```python
class Solution:
    def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
        time = [ dist[i] / speed[i] for i in range(len(dist))]
        time.sort()

        for i in range(len(time)):
            if time[i] <= i:
                return i
        return len(time)
```