# Swap Nodes [Algo]

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/jumping-on-the-clouds/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=warmup&isFullScreen=true)

  
  

## Solution:

Simple DP question. Since jumps can only be 1-2, dp size can be reduced to 2.


  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the jumpingOnClouds function below.
def jumpingOnClouds(c):
    # store our minimun steps reaching last cloud and one before that
        # prefill with 0 and 1
    jumpOne = 1
    jumpTwo = 0
    for i in range(2, len(c)):
        if c[i-1] == 0 and c[i-2] == 0:
            # can jump from both last cloud or the cloud before, pick the one with less jumps
            curr = min(jumpOne, jumpTwo) + 1
        elif c[i-1] == 1 and c[i-2] == 0:
            # must skip last cloud, jump from the one before that
            curr = jumpTwo + 1
        elif c[i-1] == 0 and c[i-2] == 1:
            # must jump form last cloud, the one before that is unlandable
            curr = jumpOne + 1
        else:
            # no way we can jump to this cloud
            return 0
        # make the jump
        jumpOne, jumpTwo= curr, jumpOne
    # we made a extra jump in the end
    return jumpOne


if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    c = list(map(int, input().rstrip().split()))

    result = jumpingOnClouds(c)

    fptr.write(str(result) + '\n')

    fptr.close()


```
**Complexity Analysis**
TC:O(n) all clouds need to be looped
SC:O(1) dp space can be 2