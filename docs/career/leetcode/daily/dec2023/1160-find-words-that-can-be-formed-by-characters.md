---
date:
    created: 2023-12-02
    updated: 2023-12-02

description: >
    Solution for Leet Code 1160. Find Words That Can Be Formed by Characters

tags:
    - LeetCode

comments: true
---
# 1160. Find Words That Can Be Formed by Characters

## Description

Given a list of words and a string, `chars`. We are asked to find the total sum of words that can be formed by `chars`

## Code

Just do it intuitively.

```python
class Solution:
    def countCharacters(self, words: List[str], chars: str) -> int:
        ans = 0
        s = {}
        for char in chars:
            if char not in s:
                s[char] = 0
            s[char] += 1
        for word in words:
            if self.formable(word, s.copy()):
                ans += len(word)
        return ans

    def formable(self, word, s):
        for char in word:
            if char not in s or s[char] < 1:
                return False
            s[char] -= 1
        return True
```