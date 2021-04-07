
# Minimum Time Required

  

## Question:

  

[Question link](https://www.hackerrank.com/challenges/minimum-time-required/problem?h_l=interview&isFullScreen=true&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=search)

  
  
  

## Solution:

At first it seems like we need to find LCM(least common multiple) of all duration for machines. at each LCM duration, we will produce same amount of products. Then for the reminder, we can linear search to produce those.

  

However, getting LCM(least common multiple) is complicated and take O(n) to do between 2 element. In this case we have n elements, O(n*n!) is expected.

  

As we know the fastest and slowest machine in our machine list, to get our target products, we can calculate our lower and upper bound for days spent. With that, we can utilize binary search to get target products. One thing to pay attention is that we could have same production for different days, so we need to travel to the front til we get the lowest days that produces target amount of products

  
  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the minTime function below.
def minTime(machines, goal):
    def getTotalProduct(produceDict, totalDays):
        total = 0
        for duration in produceDict.keys():
            total += totalDays//duration*produceDict[duration]
        return total
    produceDict, maxDuration, minDuration = {}, max(machines), min(machines)
    for day in machines:
        if day not in produceDict:
            produceDict[day] = 0
        produceDict[day] += 1
    # we try to find the minium day between our upper and lower bounds
    left, right = goal*minDuration//len(machines), maxDuration*goal//len(machines)
    while left + 1 < right:
        mid = (left+right)//2
        currProduction = getTotalProduct(produceDict, mid)
        print(left, mid, right)
        if currProduction > goal:
            right = mid
        elif currProduction < goal:
            left = mid
        else:
            # if we find days that exact match production, we try to go as low as possible
            while getTotalProduct(produceDict, mid) == currProduction:
                mid-=1
            return mid+1
    # If we fail to find one, we need to produce more than target
    return max(left, right)
        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nGoal = input().split()

    n = int(nGoal[0])

    goal = int(nGoal[1])

    machines = list(map(int, input().rstrip().split()))

    ans = minTime(machines, goal)

    fptr.write(str(ans) + '\n')

    fptr.close()


```

**Complexity Analysis**

TC:O(logn) binary search

SC:O(n) Dict to keep machine info