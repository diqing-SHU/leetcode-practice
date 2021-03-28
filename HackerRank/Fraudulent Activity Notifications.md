# Fraudulent Activity Notifications


## Question:

[Question link](https://www.hackerrank.com/challenges/fraudulent-activity-notifications/problem?h_l=interview&h_r%5B%5D%5B%5D=next-challenge&h_r%5B%5D%5B%5D=next-challenge&h_r%5B%5D%5B%5D=next-challenge&h_v%5B%5D%5B%5D=zen&h_v%5B%5D%5B%5D=zen&h_v%5B%5D%5B%5D=zen&isFullScreen=true&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=sorting)



## Solution:
If we sort on every subarray, we will have explosive run time. Sort will take O(dlogd)for each subarray. Times our one pass, time will be O(ndlogd) => O(n^2logn)

Using a dict will reduce lookup time, but won't help anything else. However, if we think about it, it's not necessary to sort subarray in order to get median as we know the numbers are all in range of [0, 200]. Thus, we can just go from 0 to 200 and count the appearance of that num we have in our dict. In this way, we reduce our time complexity to n*200 => O(n)

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the activityNotifications function below.
def activityNotifications(expenditure, d):
    # dict to store trailing unique value with count
    freq = {}
    notify=0
    # find value for idx-th item
    def find(idx):
        total_count = 0
        # start from lower value to max value
        for i in range(201):
            # if we have this value, count its appearance in dict
            if i in freq:
                total_count = total_count + freq[i]
            # if the desired item is with in this values range
            if total_count >= idx:
                # return this value
                return i
    for i in range(len(expenditure)-1):
        # add the new element in
        if expenditure[i] in freq:
            freq[expenditure[i]]+=1
        else:
            freq[expenditure[i]]=1
        # start to look if we have finished building trailing
        if i>=d-1:
            # get median with median index
            if d%2 ==0:
                median = (find(d//2)+find(d//2+1))/2
            else:
                median = find(d/2)
            if expenditure[i+1]>= (median*2) :
                notify +=1
            #remove the previous element from dictionary
            freq[expenditure[i-d+1]]-=1

    return notify  
    
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nd = input().split()

    n = int(nd[0])

    d = int(nd[1])

    expenditure = list(map(int, input().rstrip().split()))

    result = activityNotifications(expenditure, d)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) find() has time complexity of O(1), we only need to one pass all elements
SC:O(d) have a dict that holds up to d unique values