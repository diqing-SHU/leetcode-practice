# Sorting: Bubble Sort



## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-bubble-sort/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=sorting&isFullScreen=true)

  
  

## Solution:
Plain bubble sort that doesn't stop early.

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the countSwaps function below.
def countSwaps(a):
    numOfSwap = 0
    for i in range(len(a)):
        for j in range(len(a)-1):
            if a[j] > a[j+1]:
                a[j], a[j+1] = a[j+1], a[j]
                numOfSwap+=1
    print('Array is sorted in {0} swaps.'.format(numOfSwap))
    print('First Element: {0}'.format(a[0]))
    print('Last Element: {0}'.format(a[-1]))
    return

if __name__ == '__main__':
    n = int(input())

    a = list(map(int, input().rstrip().split()))

    countSwaps(a)
```
**Complexity Analysis**
TC:O(n^2) 2 nested loops and won't stop early
SC:O(1) no extra space used