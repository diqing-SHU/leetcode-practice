# Luck Balance


## Question:

[Question link](https://www.hackerrank.com/challenges/luck-balance/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=greedy-algorithms&isFullScreen=true)

  
  

## Solution:

Greedy approach. We can fail all non-important tests. Then we only pass k important tests with lowest luck spending and fail the rest to get maxium luck balance in the end.
Luck can go below 0 in the process so we don't need to worry about order of test.

  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the luckBalance function below.
def luckBalance(k, contests):
    importantList, res = [], 0
    for contest in contests:
        if contest[1] == 1:
            importantList.append(contest[0])
        else:
            # fail all non-important tests
            res+=contest[0]
    importantList.sort()
    cantFail = len(importantList) - k
    for luck in importantList:
        # spend luck on test with smaller luck requirement
        if cantFail>0:
            res-=luck
            cantFail-=1
        # fail the res
        else:
            res+=luck
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    nk = input().split()

    n = int(nk[0])

    k = int(nk[1])

    contests = []

    for _ in range(n):
        contests.append(list(map(int, input().rstrip().split())))

    result = luckBalance(k, contests)

    fptr.write(str(result) + '\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(nlogn) loop will take O(n) time. Sorting will take up to O(nlogn)
SC:O(n) Important test array size can go up to n