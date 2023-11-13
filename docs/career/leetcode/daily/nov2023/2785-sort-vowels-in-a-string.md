---
date:
  created: 2023-11-13
  updated: 2023-11-13

tags:
    - LeetCode

comments: true
---
# 2785. Sort Vowels in a String

## Description

The problem want to sort the characters of vowels in the string only in ASCII order. The vowels include the lowercases and the uppercases, i.e. `AEIOUaeiou`.

## Intuition

1. Find all the vowels with positions and numbers.
2. Loop the collected number table of vowels to place them by position.

## Code

```python
class Solution:
    def sortVowels(self, s: str) -> str:
        vowels = ['A', 'E', 'I', 'O', 'U', 'a', 'e', 'i', 'o', 'u']
        # record the numbers of vowels and their positions
        table = {v: 0 for v in vowels}
        places = []
        for i, c in enumerate(s):
            if c in vowels:
                table[c] += 1
                places.append(i)

        start = 0
        s = list(s)
        # replace by position
        for v in vowels:
            for i in places[start: start + table[v]]:
                s[i] = v
            start += table[v]
        return "".join(s)
```