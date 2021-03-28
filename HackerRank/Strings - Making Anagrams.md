# Strings: Making Anagrams

## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-making-anagrams/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=strings&isFullScreen=true)



## Solution:
store appearances in a dict. we can reduce look up time for every char.


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the makeAnagram function below.
def makeAnagram(a, b):
    appearanceDict, numOfDeletion = {}, 0
    for char in a:
        if char not in appearanceDict:
            appearanceDict[char] = 0
        appearanceDict[char] += 1
    for char in b:
        if char not in appearanceDict or appearanceDict[char] == 0:
            numOfDeletion+=1
        else:
            appearanceDict[char]-=1
    # count remaining from a that needs to be removed
    for count in appearanceDict.values():
        if count > 0:
            numOfDeletion+= count
    return numOfDeletion

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    a = input()

    b = input()

    res = makeAnagram(a, b)

    fptr.write(str(res) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) one pass on both of string
SC:O(1) extra dict size can be up to 26