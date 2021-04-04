# Greedy Florist


## Question:

[Question link](https://www.hackerrank.com/challenges/greedy-florist/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=greedy-algorithms&isFullScreen=true&h_r=next-challenge&h_v=zen)

  
  

## Solution:

Greedy approach. 
3 situations to consider

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the getMinimumCost function below.
def getMinimumCost(k, c):
    roundsBrought, itemsLeft = k//len(c), k%len(c)
    if roundsBrought == 0 and itemsLeft == 0:
        # we can brought all in one round
        return sum(c)
    elif roundsBrought == 0:
        # we have more flower than customers
        c.sort(reverse=True)
        # buy the expensice ones with original price and the rest with raised price
        purchased, cusLeftInCurrRound, res = 0, k, 0
        for cost in c:
            if cusLeftInCurrRound == 0:
                cusLeftInCurrRound = k
                purchased+=1
            cusLeftInCurrRound-=1
            res+=cost*(purchased+1)
        return res
    else:
        # we have more customers than flowers
        costPerRound = sum(c)
        c.sort()
        # buy the expensice ones with original price and the rest with raised price
        roundsBrought, itemsLeft = k//len(c), k%len(c)
        costPerRound = sum(c)
        res = costPerRound*(roundsBrought+1)*roundsBrought//2
        for cost in c:
            if itemsLeft == 0:
                break
            itemsLeft-=1
            res+=cost*(roundsBrought+1)
        return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nk = input().split()

    n = int(nk[0])

    k = int(nk[1])

    c = list(map(int, input().rstrip().split()))

    minimumCost = getMinimumCost(k, c)

    fptr.write(str(minimumCost) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) loop will take O(n) time. Sorting will take up to O(nlogn)
SC:O(n) Important test array size can go up to n