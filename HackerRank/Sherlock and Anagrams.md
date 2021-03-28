# Sherlock and Anagrams



## Question:

[Question link](https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=dictionaries-hashmaps&isFullScreen=true&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen)

  
  

## Solution:

For each Anagrams variant of same string, we should save them as same keys into our dict. Cause in order to calculate the ans. we need to calculate combinations of choosing 2 from appearance of all Anagrams variant of same string. We can sort them to get the unified version as key to store.

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the sherlockAndAnagrams function below.
def sherlockAndAnagrams(s):
    # helper function that unify the Anagrams of string to same sorted variant
    def unifyAnagrams(string):
        res = ''.join(sorted(string))
        return res
    appearanceDict, ans = {}, 0
    # first we collect appearance for unifyAnagrams version of all substrings
    # the length we can have is from 1 to len(s)
    for length in range(1,len(s)+1):
        i = 0
        while i+length<=len(s):
            curr = s[i:i+length]
            unifiedAnagrams = unifyAnagrams(curr)
            print(curr, unifiedAnagrams)
            # store corresponding appearance
            if unifiedAnagrams not in appearanceDict:
                appearanceDict[unifiedAnagrams] = 0
            appearanceDict[unifiedAnagrams] += 1
            i+=1
    for unifiedAnagrams in appearanceDict.keys():
        if appearanceDict[unifiedAnagrams] >= 2:
            # here we need to calculate the combinations for choosing two from this unifiedAnagrams
            ans += appearanceDict[unifiedAnagrams]*(appearanceDict[unifiedAnagrams]-1)//2
    return ans
    
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        s = input()

        result = sherlockAndAnagrams(s)

        fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n^3*logn) unify helper function taks O(nlogn) time as it sorts the string. loop through all substrings takes O(n^2) time as we have nested loops
SC:O(n) size of dict can go up to n