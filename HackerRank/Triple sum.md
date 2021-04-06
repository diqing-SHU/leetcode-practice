# Triple sum


## Question:

[Question link](https://www.hackerrank.com/challenges/triple-sum/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=search&isFullScreen=true)

  
  

## Solution:

Remove duplicate and sort a, b, c array. Then one pass b, for every unique b value, find possible a and c values. Add corresponding combinations to res

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the triplets function below.
def triplets(a, b, c):
    # remove dup and sort
    noDupSortedA = sorted(set(a))
    noDupSortedB = sorted(set(b))
    noDupSortedC = sorted(set(c))
    pA, pB, pC = 0, 0, 0
    possibleInA, possibleInC, res = 0, 0, 0
    while pB < len(noDupSortedB):
        while pA < len(noDupSortedA) and noDupSortedA[pA]<=noDupSortedB[pB]:
            pA+=1
            possibleInA+=1
        while pC < len(noDupSortedC) and noDupSortedC[pC]<=noDupSortedB[pB]:
            pC+=1
            possibleInC+=1
        res+=possibleInA*possibleInC
        pB+=1
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    lenaLenbLenc = input().split()

    lena = int(lenaLenbLenc[0])

    lenb = int(lenaLenbLenc[1])

    lenc = int(lenaLenbLenc[2])

    arra = list(map(int, input().rstrip().split()))

    arrb = list(map(int, input().rstrip().split()))

    arrc = list(map(int, input().rstrip().split()))

    ans = triplets(arra, arrb, arrc)

    fptr.write(str(ans) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) used sort wich takes longer
SC:O(n) build a sorted set of our a, b, c array