# Merge Sort: Counting Inversions

## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-merge-sort/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=sorting&isFullScreen=true)



## Solution:
If we use bubble sort, the swapping behavior matches. But the run time is O(n^2) and that's not good. We need to use merge sort which has time complexity of O(nlogn).

The hard thing is how to track swaps in this case. Since we are only allow to swap with adjacent element, when we put element back to correct position we need to do n swaps to travel the n gaps between its curr postion


```python
#!/bin/python3
#!/bin/python3

import math
import os
import random
import re
import sys

count = 0

def mergesort2(A):
    global count
    # if subarray is longer than 1, we need to sort
    if len(A) > 1:
        # keep dividing the array
        n = len(A)
        m = n//2
        L = A[:m]
        R = A[m:n]
        # recursive call on divided subarraies
        # to make sure they are sorted
        mergesort2(L)
        mergesort2(R)
        # merge the 2 sorted arraies
        i = 0
        j = 0
        k = 0
        n1 = m
        n2 = n-m
        
        while i < n1 and j < n2:
            # element on the left half is smaller, put it in first (index is not changed)
            if L[i] <= R[j]:
                A[k] = L[i]
                i += 1
                k += 1
            # element on the right half is smaller, put it in first (move to left half, index is changed)
            else:
                A[k] = R[j]
                j += 1
                k += 1
                # the accrual distance is n1-i, as previous element smaller on the right side has been moved 
                # R[j] is the first of R the index for it is n1, i is the curr index of target
                count += n1-i
        # put the rest in
        while i < n1:
            A[k] = L[i]
            i+=1
            k+=1 
        while j < n2:
            A[k] = R[j]
            j+=1
            k+=1


# Complete the countInversions function below.
def countInversions(arr):
    global count
    count = 0
    mergesort2(arr)
    return count

        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    t = int(input())

    for t_itr in range(t):
        n = int(input())

        arr = list(map(int, input().rstrip().split()))

        result = countInversions(arr)

        fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(nlogn) merge sort has better time complexity
SC:O(n) function call stack