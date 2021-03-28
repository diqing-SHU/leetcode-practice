# Frequency Queries



## Question:

[Question link](https://www.hackerrank.com/challenges/frequency-queries/problem?h_l=interview&isFullScreen=true&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D%5B%5D%5B%5D=dictionaries-hashmaps&h_r=next-challenge&h_v=zen)

  
  

## Solution:
Dict to store the freq of each value is a must. Another dict to store count for each freq seems to solve the timeout issue. Not sure if there is a better solution

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the freqQuery function below.
def freqQuery(queries):
    res = []
    appearanceDict = {}
    freqDict = {}
    for query in queries:
        if query[0] == 1:
            # update freq
            if query[1] not in appearanceDict:
                appearanceDict[query[1]] = 0
            appearanceDict[query[1]] += 1
            # count this freq in
            if appearanceDict[query[1]] not in freqDict:
                freqDict[appearanceDict[query[1]]] = 0
            freqDict[appearanceDict[query[1]]]+=1
            # remove 1 from old freq
            if appearanceDict[query[1]]-1 in freqDict and freqDict[appearanceDict[query[1]]-1] > 0:
                freqDict[appearanceDict[query[1]]-1] -= 1
        elif query[0] == 2:
            # update freq
            if query[1] in appearanceDict and appearanceDict[query[1]] > 0:
                appearanceDict[query[1]] -= 1
                # count this freq in
                if appearanceDict[query[1]] not in freqDict:
                    freqDict[appearanceDict[query[1]]] = 0
                freqDict[appearanceDict[query[1]]]+=1
                # remove 1 from old freq
                if appearanceDict[query[1]]+1 in freqDict and freqDict[appearanceDict[query[1]]+1] > 0:
                    freqDict[appearanceDict[query[1]]+1] -= 1
        elif query[0] == 3:
            # look up for that freq
            if query[1] in freqDict and freqDict[query[1]] > 0:
                res.append(1)
            else:
                res.append(0)
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input().strip())

    queries = []

    for _ in range(q):
        queries.append(list(map(int, input().rstrip().split())))

    ans = freqQuery(queries)

    fptr.write('\n'.join(map(str, ans)))
    fptr.write('\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(q) all queries need to be performed. Lookup time is O(1) through
SC:O(q) size of each dict can go up to q