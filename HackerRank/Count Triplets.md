# Count Triplets



## Question:

[Question link](https://www.hackerrank.com/challenges/count-triplets-1/problem?h_l=interview&isFullScreen=true&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=dictionaries-hashmaps)

  
  

## Solution:
Since indexes of geometric progression triplets are always in increasing order. While we loop through the arr, we can build and store appearance of elements as well as partial possible triplet. The data stored in the Hashmap can be used to determine if we finished a triplets with curr num as well as how many of such triplets ending at this index we have

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the countTriplets function below.
def countTriplets(arr, r):
    appearanceDict = {}
    ans = 0
    for num in arr:
        # set up variables
        prev1, prev2 =0, 0
        # check if num can be the third of any geometric progression
        if num%r == 0:
            prev1 = num//r
            if prev1%r == 0:
                prev2 = prev1//r
        # if so check and add to our res
        if prev1 > 0 and prev2 > 0:
            # check if we have partial triplet to create geometric progression
            if (prev2,prev1) in appearanceDict:
                # add possible combinations
                print(prev2,prev1,num)
                print(appearanceDict[(prev2,prev1)])
                ans+=appearanceDict[(prev2,prev1)]
        # chcek if we can create partial triplet
        if prev1 > 0 and prev1 in appearanceDict:
            if (prev1,num) not in appearanceDict:
                appearanceDict[(prev1,num)] = 0
            appearanceDict[(prev1,num)] += appearanceDict[prev1]
        # finish calculation for curr num
        # put curr num in for later
        if num not in appearanceDict:
            appearanceDict[num] = 0
        appearanceDict[num]+=1
    return ans

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nr = input().rstrip().split()

    n = int(nr[0])

    r = int(nr[1])

    arr = list(map(int, input().rstrip().split()))

    ans = countTriplets(arr, r)

    fptr.write(str(ans) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) one loop through all elements will be fine
SC:O(n) size of dict can go up to 2n, since it contains both elements and partial triplets