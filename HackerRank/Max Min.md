# Max Min


## Question:

[Question link](https://www.hackerrank.com/challenges/angry-children/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=greedy-algorithms&isFullScreen=true)



## Solution:
If we sort the array. max - min becomes element at index i - element at index i-(k-1), since all elements are in increasing order.


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maxMin function below.
def maxMin(k, arr):
    # sort array first
    sortedArr, res = sorted(arr), float('inf')
    for i in range(k-1, len(sortedArr)):
        res = min(res, sortedArr[i] - sortedArr[i-k+1])
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    k = int(input())

    arr = []

    for _ in range(n):
        arr_item = int(input())
        arr.append(arr_item)

    result = maxMin(k, arr)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) we sort the array and then one pass
SC:O(1) no extra space if mutation of data is allowed