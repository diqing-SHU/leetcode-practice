# Mark and Toys


## Question:

[Question link](https://www.hackerrank.com/challenges/mark-and-toys/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=sorting&isFullScreen=true&h_r=next-challenge&h_v=zen)



## Solution:
Go greedy on the sorted array.

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maximumToys function below.
def maximumToys(prices, k):
    res = 0
    for price in sorted(prices):
        k -= price
        if k < 0:
            return res
        res+=1
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nk = input().split()

    n = int(nk[0])

    k = int(nk[1])

    prices = list(map(int, input().rstrip().split()))

    result = maximumToys(prices, k)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) python built-in sort have a O(nlogn) TC (Tim Sort)
SC:O(n) sorted creates a new list