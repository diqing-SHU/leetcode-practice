# Max Array Sum

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/max-array-sum/)

  
  

## Solution:

DP solution. Not much to say. Two things to notice:

1. we can choose 0 (not picking the item)
2. dp[1] we can choose max from arr[0], arr[1] and 0

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maxSubsetSum function below.
def maxSubsetSum(arr):
    if len(arr)<=2:
        return max(arr)
    # 2 dp values will be enough
    # on dpPrev1, we can choose between arr[1], arr[0] and 0 
    dpPrev1, dpPrev2 = max(arr[1], arr[0], 0), max(arr[0], 0)
    dp = [0]*len(arr)
    for i, num in enumerate(arr):
        if i > 1:
            # only need to add num that is above 0
            # update our dpPrev1 and dpPrev2
            dpPrev1, dpPrev2 = max(dpPrev1, dpPrev2+max(num, 0)), dpPrev1
    # we can also choose to add no number
    return dpPrev1

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    arr = list(map(int, input().rstrip().split()))

    res = maxSubsetSum(arr)

    fptr.write(str(res) + '\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(n) Need to loop through every element
SC:O(1) Constant dp space used