# Max deviation among all substrings

## Question

[Question link](https://leetcode.com/discuss/interview-question/1742621/Amazon-or-OA-or-Max-deviation-among-all-substrings)

Let's have a string: abbbcacbcdce

For substring abbb, you have most frequent letter b -> 3 and least frequent letter a -> 1.
So the deviation is = most frequent - least frequent = 3 - 1 = 2. You need to look at all the substrings and find the max deviation.

Here substring cacbcdc has the max deviation.
Frequency is like below:
c -> 4, a ->1, b->1, d->1.
So max freq - min freq = 4 - 1 = 3.

Among all substrings deviation, this is the max. So need to return it.

String length is 10^4. So you can't check each substring.

## Solution

```python
# abbbcacbcdce
def singleMaxDeviation(string, char1, char2):
    countArray = []
    char2Count, res = 0, 0
    # build count array(merge counts for same elements in a row)
    # use -/+ 1 for easy counting
    for char in string:
        if char == char1:
            if len(countArray) == 0:
                countArray.append(1)
            else:
                if countArray[-1]>0:
                    countArray[-1]+=1
                else:
                    countArray.append(1)
        if char == char2:
            if len(countArray) == 0:
                countArray.append(-1)
            else:
                if countArray[-1]<0:
                    countArray[-1]-=1
                else:
                    countArray.append(-1)
    # get max sum of length over 1(we need to have at least one of each element)
    dp = countArray[0]
    for i in range(1, len(countArray)):
        count = countArray[i]
        dp = max(dp+count, count+countArray[i-1])
        res = max(dp, res)
    return res
def maxDeviation(string):
    allChars = list(set([char for char in string]))
    res = 0
    for i in range(len(allChars)):
        for j in range(i+1, len(allChars)):
            res = max(singleMaxDeviation(string, allChars[i], allChars[j]), singleMaxDeviation(string, allChars[j], allChars[i]), res)
    return res
print(maxDeviation("abbbcacbcddcee"))
print(maxDeviation("abbbcacbcdcefghijklmn"))
print(maxDeviation("ababcac"))
```

**Complexity Analysis**
TC:O(2*26*26*n) The 2 nested for loops for maxDeviation takes `O(26)` each. We make 2 of `singleMaxDeviation` calls in each iteration which is `O(n)` since it one passes the string.
SC:O(2*26*26*n) extra space to store Count array for `singleMaxDeviation`.
