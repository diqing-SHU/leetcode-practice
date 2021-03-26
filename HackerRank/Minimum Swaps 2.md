# Minimum Swaps 2



## Question:

[Question link](https://www.hackerrank.com/challenges/minimum-swaps-2/problem?isFullScreen=true)

  
  

## Solution:

First lower value to match with indexes. Create a HashMap to hold current index for values to save look up time. Then we just perform swap for each value in the loop.

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the minimumSwaps function below.
def minimumSwaps(arr):
    res = 0
    valueIndexMap = {}
    # build our valueIndexMap
    for i in range(len(arr)):
        # lower the value to match with index
        arr[i] -= 1
        # put value and curr index to our dict
        valueIndexMap[arr[i]] = i
        
    for i in range(len(arr)):
        print(i, arr[i])
        if i != arr[i]:
            currIndex = valueIndexMap[i]
            # swap the value
            arr[currIndex], arr[i] = arr[i], arr[currIndex]
            # update valueIndexMap based on new index for those values
            valueIndexMap[arr[i]], valueIndexMap[arr[currIndex]] = i, currIndex
            # record this swap
            res += 1
    return res
            

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    arr = list(map(int, input().rstrip().split()))

    res = minimumSwaps(arr)

    fptr.write(str(res) + '\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(n) Max swaps we can have is n times
SC:O(n) used a hashmap with same size of the list