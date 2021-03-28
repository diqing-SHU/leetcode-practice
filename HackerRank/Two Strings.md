# Two Strings


## Question:

[Question link](https://www.hackerrank.com/challenges/two-strings/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=dictionaries-hashmaps&isFullScreen=true&h_r=next-challenge&h_v=zen)

  
  

## Solution:

Use HashMap to trade lookup time with space.

```python
#!/bin/python3

import math
import os
import random
import re
import sys
# import for using counter
import collections

# Complete the twoStrings function below.
def twoStrings(s1, s2):
    # if we have 1 common char from both string
    # we can return true
    # only if there are only unique chars
    # we return false
    siCharCounter = collections.Counter(s1)
    for char in s2:
        if char in siCharCounter:
            return "YES"
    return "NO"
    

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s1 = input()

        s2 = input()

        result = twoStrings(s1, s2)

        fptr.write(result + '\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(m or n) greater one of m and n will be our time complexity
SC:O(m) used a hashmap to store char appearance of s1