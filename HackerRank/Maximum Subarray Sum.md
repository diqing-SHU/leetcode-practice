# Maximum Subarray Sum

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/maximum-subarray-sum)

  
  

## Solution:
Before getting into the correct solution, we all know there is a O(n^2) algorithm to solve it. We call that Brutal Force solution(BF)

To solve it in a better way, the problem requires some knowledge of modular arithmetic.
Here are some basic formula for this problem:
(a+b)%M=(a%M+b%M)%M  --- 1
(a−b)%M=(a%M−b%M)%M  --- 2

Now, let's solve the problem with the simple math formula!

Usually, a great many problems related to "subarray computation" could be solved with prefix array, which saves time for repeating computation.
Define:
prefix[n]=(a[0]+a[1]+...+a[n])%M

The we have to find a subarray. Any subarray can be expressed in the following way:
sumModular[i,j]=(prefix[j]−prefix[i−1]+M)%M  --3

which is very simple and efficient.
The correctness of 3 require some math based on 1 and 2. And 3 is the key to the efficient solution!

if prefix[j] is smaller than prefix[i], in the previous code, there is no need to calculate, because for prefix[j] < prefix[i], we have:
(prefix[i]−prefix[j]+M)%M=prefix[i]−prefix[j]≤prefix[i] 

So we just need to find those j, which prefix[j] > prefix[i]. Ok, let's just linear scan all j before i and find the ones that is smaller than prefix[i]. But that makes no difference in terms of time complexity.

To further reduce the time, we need the prefix structure to be sorted.

---

Thus, we can sum up our thoughts and give it a shot.

First of all, we need to construct our prefix array, we need to include index as we will be using it to verify whether our range is valid later.

Then the key-logic is, if the larger index(say j) has smaller prefix_sum than any smaller index (say i), then that sub-array (from i to j) can be a contender for our solution provided it's sum%m is maximum.

Therefore, we can sort the prefix array based on prefix_sum, so that we can be sure that the max prefix_sum smaller than curr one is the one before it.

Now, we have to find the minimum difference b/w all the prefix_sum % m, such that the first one's index is larger than the latter one's index

We can easily achieve that with our sorted prefix.


```python
#!/bin/python3
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the maximumSum function below.
def maximumSum(a, m):
    # if we build the perfix array, we can resuce our calculations
    prefixArray, prev, res = [], 0, float('-inf')
    for i, num in enumerate(a):
        prev = (prev+num)%m
        res = max(res, prev)
        prefixArray.append((prev, i))
    # sort our prefixArray, so that
    # the prev is in ascending order
    # while i remains ascending for same prefix_sum
    prefixArray.sort()
    # loop prefixArray reversely to
    # make sure we have descending pot
    for start in range(len(a)-1,0,-1):
        pot, pos = prefixArray[start]
        # pot_prev will be the max val
        # thats smaller than pot
        # in other words, we have min difference
        pot_prev, pos_prev = prefixArray[start-1]
        # we must have pos_prev > pos (i < j, range is valid)
        if pos_prev > pos:
            # check if this is our new max
            candidate = (pot_prev - pot) % m
            res = max(res, candidate)
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    q = int(input())

    for q_itr in range(q):
        nm = input().split()

        n = int(nm[0])

        m = int(nm[1])

        a = list(map(int, input().rstrip().split()))

        result = maximumSum(a, m)

        fptr.write(str(result) + '\n')

    fptr.close()

```
**Complexity Analysis**
TC:O(n) Need to loop through every element of the 2d array
SC:O(1) Constant space used