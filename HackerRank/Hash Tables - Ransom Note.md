# Hash Tables: Ransom Note




## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-ransom-note/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=dictionaries-hashmaps&isFullScreen=true)

  
  

## Solution:

Use HashMap to trade lookup time with space.

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the checkMagazine function below.
def checkMagazine(magazine, note):
    # build our dict
    magazineDict = {}
    for word in magazine:
        if word not in magazineDict:
            magazineDict[word] = 0
        magazineDict[word] += 1
    for word in note:
        if word not in magazineDict or magazineDict[word] == 0:
            print("No")
            return
        magazineDict[word] -= 1
    print("Yes")
    return
    

if __name__ == '__main__':
    mn = input().split()

    m = int(mn[0])

    n = int(mn[1])

    magazine = input().rstrip().split()

    note = input().rstrip().split()

    checkMagazine(magazine, note)
```
**Complexity Analysis**
TC:O(m or n) greater one of m and n will be our time complexity
SC:O(m) used a hashmap to store notes