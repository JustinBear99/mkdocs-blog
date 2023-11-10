---
date:
  created: 2023-11-10
  updated: 2023-11-10

tags:
    - LeetCode

comments: true
---

# 1743. Restore the Array From Adjacent Pairs

## Description

The original array was separated into the adjacent pairs. Since it's a 1-d array, except for the start and the end, every elemnt has two adjacent neighbors. To keep track of the relations, the common approach is to use hash map. 

We can expect that the start and the end can only map to 1 element and all the other elements can map to 2 elements.

## Intuition

1. Build hash map for every pair. For example, pair = [a, b], then link a to b and b to a.
2. Find an **end** for the original array.
3. Rebuild the array recursively by the hash map

## Code

```python
class Solution:
    def restoreArray(self, adjacentPairs: List[List[int]]) -> List[int]:
        # build hash map
        table = {}
        for i, j in adjacentPairs:
            if i not in table:
                table[i] = []
            if j not in table:
                table[j] = []
            table[i].append(j)
            table[j].append(i)
        # find an end
        ans = []
        for k, v in table.items():
            if len(v) == 1:
                ans.append(k)
                ans.append(table[k][0])
                break
        # reconstruct the array
        while True:
            last = ans[-1]
            vals = table[last]
            if len(vals) == 1:
                # the other end found
                break
            # find the other adjacent
            elif vals[0] != ans[-2]:
                ans.append(vals[0])
            else:
                ans.append(vals[1])
        return ans
```