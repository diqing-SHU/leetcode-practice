# Alternating Characters

## Question:

[Question link](https://www.hackerrank.com/challenges/alternating-characters/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=strings&isFullScreen=true&h_r=next-challenge&h_v=zen)



## Solution:
One pass the string while comparing with prev element


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the alternatingCharacters function below.
def alternatingCharacters(s):
    prev, numOfDelete = None, 0
    for char in s:
        if prev:
            if prev == char:
                numOfDelete+=1
        # put curr char in
        prev = char
    return numOfDelete

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s = input()

        result = alternatingCharacters(s)

        fptr.write(str(result) + '\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(n) one pass string
SC:O(1) no extra space