---
date:
    created: 2023-12-17
    updated: 2023-12-17

description: >
    Solution for Leet Code 2353. Design a Food Rating System

tags:
    - LeetCode

comments: true
---
# 2353. Design a Food Rating System

## Descrption

Design a class that holds food rating information and provide method for updating and getting the info.

## Intuition

Since `changeRating()` and `highestRated()` take in `food` and `cuisine` respectively, we can use map to mapping those relation. For finding the highest rating from given food name, we best use heap (priosity queue) or any ordered data structure. Here, I use `SortedSet` because we would like to change the state of sorted element and is not suitable for queue.

## Code

```python
from sortedcontainers import SortedSet

class FoodRatings:

    def __init__(self, foods: List[str], cuisines: List[str], ratings: List[int]):
        self.cuisineMap = defaultdict(SortedSet)
        self.food2cuisine = {}
        self.food2rating = {}
        for i in range(len(foods)):
            f, c, r = foods[i], cuisines[i], ratings[i]
            self.cuisineMap[c].add((-r, f))
            self.food2cuisine[f] = c
            self.food2rating[f] = -r

    def changeRating(self, food: str, newRating: int) -> None:
        c = self.food2cuisine[food]
        foodSet = self.cuisineMap[c]
        old = (self.food2rating[food], food)
        foodSet.remove(old)
        foodSet.add((-newRating, food))
        self.food2rating[food] = -newRating

    def highestRated(self, cuisine: str) -> str:
        c = self.cuisineMap[cuisine]
        return c[0][1]


# Your FoodRatings object will be instantiated and called as such:
# obj = FoodRatings(foods, cuisines, ratings)
# obj.changeRating(food,newRating)
# param_2 = obj.highestRated(cuisine)
```