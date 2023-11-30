---
date:
    created: 2023-11-30
    updated: 2023-11-30

description: >
    Solution for Leet Code 191. Number of 1 Bits

tags:
    - LeetCode

comments: true
---
# 1611. Minimum One Bit Operations to Make Integers Zero

## Description

Given two operations:

1. Change rightmost bit from `0` to `1` or from `1` to `0`
2. Change `i`th bit as the above as long as `i-1` bit is `1` and rest of `i-2` bits are `0` (indexing from right to left)

Find the minimum operations to make integer `n` to zero.

## Intuition

At first, I thought that the question can be solved by DP like `f(make n bits zero) = f(let nth bit zero) + f(make n-1 bits zero)` and can solve it bit by bit. But turns out that this approach would require a lot more analysis in detail.

Thanks to [lee's](https://leetcode.com/problems/minimum-one-bit-operations-to-make-integers-zero/solutions/877798/java-c-python-3-solutions-with-prove-o-1-space/?envType=daily-question&envId=2023-11-30) and [delphih's](https://leetcode.com/problems/minimum-one-bit-operations-to-make-integers-zero/solutions/877708/python-c-o-log-n-with-prove/?envType=daily-question&envId=2023-11-30) solutions, this problem actually requires more analysis on the recursive behaviour.

1. Symmetric: operations required to change `m` to `n` is the same as changing from `n` to `m`. i.e. `f(m->n) = f(n->m)`
2. 2^k: The operations required from `2^k` (`100..00` in binary) to `0` is calculable and is `2^(k + 1) - 1`. i.e. `f(n if n == 2^k where k is int) = 2^(k + 1) - 1`

Therefore, to solve ant given number `n` equals to sovle `1XXXXX` (in binary)

So 
```
f(100000 -> 0) = f(100000 -> 1XXXXX) + f(1XXXXX -> 0)
               = f(1XXXXX -> 100000) + f(1XXXXX -> 0)
               = f(0XXXXX -> 000000) + f(1XXXXX -> 0)
->
f(1XXXXX -> 0) = f(100000 -> 0) - f(XXXXX -> 0) 
```

## Code

```python
class Solution:
    def minimumOneBitOperations(self, n: int) -> int:
        if n == 0:
            return 0
        highest_bit = int(math.log2(n))
        return self.makeIthBitZero(highest_bit) - self.minimumOneBitOperations(n - (1 << highest_bit))
        
    @lru_cache
    def makeIthBitZero(self, i):
        return (1 << (i + 1)) - 1 # equals to 2 ** (i + 1) - 1
```

## Gray Code

This problem actually comes from [gray code](https://en.wikipedia.org/wiki/Gray_code), a special order of binary code used in some digital procressing.