# Hash Tables: Ice Cream Parlor


## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-ice-cream-parlor/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=search&isFullScreen=true)



## Solution:
This is a two sum. Keep building our visted Dict and check for remaining money in our visted Dict. Print out the pairs on the way


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the whatFlavors function below.
def whatFlavors(cost, money):
    costDict = {}
    for i, c in enumerate(cost):
        costToFind = money - c
        # check and print ans
        if costToFind in costDict:
            # index is garenteed to be smaller than i
            # as they are stored in previous iterations
            # every previous index will form a unique pair
            for index in costDict[costToFind]:
                print(index+1, i+1)
        # record curr cost to dict
        # to handle same value, we store ids in list
        if c not in costDict:
            costDict[c] = []
        costDict[c].append(i)
        

if __name__ == '__main__':
    t = int(input())

    for t_itr in range(t):
        money = int(input())

        n = int(input())

        cost = list(map(int, input().rstrip().split()))

        whatFlavors(cost, money)

```
**Complexity Analysis**
TC:O(n) One pass is enough
SC:O(n) We are building a hashmap, size up to n