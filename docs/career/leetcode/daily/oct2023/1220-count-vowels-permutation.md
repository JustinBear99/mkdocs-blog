---
date:
  created: 2023-10-28
  updated: 2023-10-28

tags:
    - LeetCode

comments: true
---

# 1220. Count Vowels Permutation

## Description

The goal is to find the number of permutations of string following the rule described in the [problem](https://leetcode.com/problems/count-vowels-permutation/description/?envType=daily-question&envId=2023-10-28).

## Intuition

Follow the rules of the problem, dynamically construt the number of string until matching requested length.

1. Initialize `count` representing the number of substring ended with `a`, `e`, `i`, `o`, `u`.
2. Loop calculate the combination with respect to the rules until length reaches `n`.

## Code
```python
class Solution:
    def countVowelPermutation(self, n: int) -> int:
        count = [1, 1, 1, 1, 1]
        while n > 1:
            count = [
                    count[1] + count[2] + count[4], # substring ended with *a* can be formed with substring ended with *e*, *i*, *u*
                    count[0] + count[2], # same logic
                    count[1] + count[3], 
                    count[2], 
                    count[2] + count[3]]
            n -= 1
        return sum(count) % (10 ** 9 + 7)
```