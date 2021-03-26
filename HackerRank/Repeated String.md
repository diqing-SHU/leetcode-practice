# Swap Nodes [Algo]

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/repeated-string/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=warmup&isFullScreen=true)

  
  

## Solution:

Get the number of repeat and length of substring remaining.
One pass the word s to get count of a in s and substring
Calculate the res


  

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the repeatedString function below.
def repeatedString(s, n):
    # get number of repeats
    repeats = n//len(s)
    # get length of remaining partial substring of s
    remaining = n%len(s)
    aCounts = 0
    extraARepeat = 0
    for char in s:
        # count the appearance of a in s
        if char == 'a':
            aCounts+=1
        if remaining > 0:
            remaining-=1
            if char == 'a':
                extraARepeat+=1
        # count the appearance of a in last partial substring of s
    return repeats*aCounts+extraARepeat
    

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    s = input()

    n = int(input())

    result = repeatedString(s, n)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) Need to loop through the word
SC:O(1) Constant space used