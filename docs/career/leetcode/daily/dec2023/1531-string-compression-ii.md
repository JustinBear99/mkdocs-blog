---
date:
    created: 2024-01-02
    updated: 2024-01-02

description: >
    Solution for Leet Code 1531. String Compression II

tags:
    - LeetCode

comments: true
---
# 1531. String Compression II

## Description

We are asked to find the minimum encoded length of `s` after removing `k` characters from it.

## Intuition

To effectively decrease the size, we may remove the character that appears once, 10 times, 100 times, etc. or removing a charactor that can let its left or right segments merged like `aaabaaa` (removing `b`). However, those are way too complicated to consider, I suggest to follow the idea from [this solution](https://leetcode.com/problems/string-compression-ii/solutions/755970/python-dynamic-programming/?envType=daily-question&envId=2023-12-28) which is quite beautiful.

## Code

```python
class Solution:
    def getLengthOfOptimalCompression(self, s: str, k: int) -> int:
        # this decorator automatically use memo with key = (start, last, last_count, left)
        @lru_cache(None)
        def counter(start, last, last_count, left): #count the cost of compressing from the start
            if left < 0:
                return float('inf') # this is impossible
            if start >= len(s):
                return 0
            if s[start] == last:
				# we have a stretch of the last_count of the same chars, what is the cost of adding one more? 
                incr = 1 if last_count == 1 or last_count == 9 or last_count == 99 else 0
				# no need to delete here, if we have a stretch of chars like 'aaaaa' - we delete it from the beginning in the else delete section
                return incr + counter(start+1, last, last_count+1, left) # we keep this char for compression
            else:
				# keep this char for compression - it will increase the result length by 1 plus the cost of compressing the rest of the string 
                keep_counter = 1 + counter(start+1, s[start], 1, left)
				# delete this char
                del_counter =  counter(start + 1, last, last_count, left - 1)
                return min(keep_counter, del_counter)
            
        return counter(0, "", 0, k)
```