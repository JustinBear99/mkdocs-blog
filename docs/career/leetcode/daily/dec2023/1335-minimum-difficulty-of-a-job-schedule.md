---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 1335. Minimum Difficulty of a Job Schedule

tags:
    - LeetCode

comments: true
---
# 1335. Minimum Difficulty of a Job Schedule

## Description

Minimize the total job effort for `d` days.

## Intuition

Similar to the problems of previous days, DP is the key to these questions. The recursive loop starts from thinking *how many jobs whould I take for a day* and let the recursive function and cache do the job. Taught by [lee's solution](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/solutions/490316/java-c-python3-dp-o-nd-solution/).

## Code

```python
class Solution:
    def minDifficulty(self, jobDifficulty: List[int], d: int) -> int:
        n = len(jobDifficulty)
        if n < d:
            return -1
        @lru_cache(None)
        def dfs(i, d):
            if d == 1:
                return max(jobDifficulty[i:])
            ret, max_d = float("inf"), 0
            for j in range(i, n - d + 1):
                max_d = max(max_d, jobDifficulty[j])
                ret = min(ret, max_d + dfs(j + 1, d - 1))
            return ret
        return dfs(0, d)
```