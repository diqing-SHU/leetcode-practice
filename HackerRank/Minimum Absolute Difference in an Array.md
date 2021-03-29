# Minimum Absolute Difference in an Array
  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/minimum-absolute-difference-in-an-array/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=greedy-algorithms&isFullScreen=true)

  
  

## Solution:

Sort and then one pass

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the minimumAbsoluteDifference function below.
def minimumAbsoluteDifference(arr):
    prev, minAbsDiff = None, float('inf')
    for num in sorted(arr):
        if prev != None:
            minAbsDiff = min(num-prev, minAbsDiff)
        prev = num
    return minAbsDiff

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    arr = list(map(int, input().rstrip().split()))

    result = minimumAbsoluteDifference(arr)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) Sorting takes longer time than one pass
SC:O(n) space used to store sorted arr. If data mutation is allowed, no extra space is needed