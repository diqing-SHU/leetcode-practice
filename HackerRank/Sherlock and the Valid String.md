# Sherlock and the Valid String

## Question:

[Question link](https://www.hackerrank.com/challenges/sherlock-and-valid-string)



## Solution:
One pass the string while comparing with prev element


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the isValid function below.
def isValid(s):
    appearanceDict, countDict = {}, {}
    # count appearance for chars
    for char in s:
        if char not in appearanceDict:
            appearanceDict[char] = 0
        appearanceDict[char] += 1
    # count different num of appeances
    for count in appearanceDict.values():
        if count not in countDict:
            if len(countDict) == 2:
                # cant fix if we gonna have more that 2 different counts
                return 'NO'
            countDict[count] = 0
        countDict[count] += 1
    # check counts, if we reach here, we should only have no more than than 2 counts in our dict
    # if len is one, counts are all the same right now
    if len(countDict) < 2:
        return 'YES'
    # if we have single appearance of one stand our element, we can just remove
    if 1 in countDict and countDict[1]==1:
        return 'YES'
    # try to fix if we have 2 different counts
    for count in countDict.keys():
        # we can possibly fix it if the difference if 1
        if count+1 in countDict:
            # we can only remove (reduce count)
            if countDict[count+1] == 1:
                return 'YES'
            return 'NO'
    return 'NO'

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    s = input()

    result = isValid(s)

    fptr.write(result + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) one pass string
SC:O(1) no extra space