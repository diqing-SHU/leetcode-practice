# Arrays: Left Rotation



## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-array-left-rotation/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=arrays&isFullScreen=true)

  
  

## Solution:

Not much, loop and use correct element to build return array

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the rotLeft function below.
def rotLeft(a, d):
    # We only need to rotate the remainder times
    numberOfRotNeeded = d%len(a)
    res = []
    for i in range(len(a)):
        originIndex = i + numberOfRotNeeded
        if originIndex < len(a):
            res.append(a[originIndex])
        else:
            res.append(a[originIndex - len(a)])
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nd = input().split()

    n = int(nd[0])

    d = int(nd[1])

    a = list(map(int, input().rstrip().split()))

    result = rotLeft(a, d)

    fptr.write(' '.join(map(str, result)))
    fptr.write('\n')

    fptr.close()


```
**Complexity Analysis**
TC:O(n) Time takes to build a output array of same size
SC:O(n) Used a output array of same size