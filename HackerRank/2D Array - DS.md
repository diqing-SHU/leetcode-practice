# 2D Array - DS

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/2d-array/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=arrays&isFullScreen=true)

  
  

## Solution:

Calculate all hourglass sums and keep track of the max one. BF solution?

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the hourglassSum function below.
def hourglassSum(arr):
    # helper function to get sum for one hourglass
    def calHourglassSum(midRow, midCol):
        return arr[midRow-1][midCol-1]+arr[midRow-1][midCol]+arr[midRow-1][midCol+1]+arr[midRow][midCol]+arr[midRow+1][midCol-1]+arr[midRow+1][midCol]+arr[midRow+1][midCol+1]
    # Calculate all hourglass and keep track of max
    maxSum = float('-inf')
    for row in range(1, len(arr)-1):
        for col in range(1, len(arr)-1):
            maxSum = max(calHourglassSum(row,col), maxSum)
    return maxSum

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    arr = []

    for _ in range(6):
        arr.append(list(map(int, input().rstrip().split())))

    result = hourglassSum(arr)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) Need to loop through every element of the 2d array
SC:O(1) Constant space used