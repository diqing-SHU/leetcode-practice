# Pairs

## Question:

[Question link](https://www.hackerrank.com/challenges/pairs/problem?h_l=interview&h_r=next-challenge&h_v=zen&isFullScreen=true&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=search&h_r=next-challenge&h_v=zen)

  
  

## Solution:

similar to 2 sum questions.

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the pairs function below.
def pairs(k, arr):
    appearedDict, res = {}, 0
    for num in arr:
        higherVal, lowerVal = num+k, num-k
        if higherVal in appearedDict:
            res+=appearedDict[higherVal]
        if lowerVal in appearedDict:
            res+=appearedDict[lowerVal]
        if num not in appearedDict:
            appearedDict[num] = 0
        appearedDict[num] += 1
    return res
        
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nk = input().split()

    n = int(nk[0])

    k = int(nk[1])

    arr = list(map(int, input().rstrip().split()))

    result = pairs(k, arr)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) one pass
SC:O(n) appearedDict can go up to n