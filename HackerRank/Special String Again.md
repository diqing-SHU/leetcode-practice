# Special String Again

## Question:

[Question link](https://www.hackerrank.com/challenges/special-palindrome-again/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=strings&isFullScreen=true&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen)



## Solution:
2 cases to handle:
- case 1: each substring with same element, we can calculate and add count for all possibilities when longest if find (next char is different)
- case 2: 2 case 1 sub string of same value with exactly one different char in bettween. we need to save 2 previous proccessed substring to check.


```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the substrCount function below.
def substrCount(n, s):
    prevElement1,prevCount1, prevElement2, prevCount2, p1, res = None, 0, None, 0, 0, 0
    while p1 < n:
        # count duplicates and
        p2 = p1
        while p2 < n and s[p1] == s[p2]:
            p2+=1
        count = p2-p1
        currElement = s[p1]
        # check our prevElement is built up
        if prevElement1 and prevElement2:
            # only need to count case 2 if there is only one mid element
            if prevCount1 == 1 and currElement == prevElement2:
                res += min(count, prevCount2)
            # store new element info
            prevElement2, prevCount2 = prevElement1, prevCount1
        # only filled prevElement1
        elif prevElement1:
            # store new element info
            prevElement2, prevCount2 = prevElement1, prevCount1
        # always fill in to prev1
        prevElement1 = currElement
        prevCount1 = count
        # also update to our case1 substrings all combination from length 1 to count
        res += count*(count+1)//2
        # move to next different element
        p1 = p2
    return res
            
        
        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    s = input()

    result = substrCount(n, s)

    fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) one pass string
SC:O(1) constant extra space