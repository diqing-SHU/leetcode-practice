# Minimum Total Container Size

## Question

[Question link](https://aonecode.com/Amazon-Online-Assessment-Minimum-Total-Container-Size)
It's basically [Minimum Difficulty of a Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/)

## Solution 1: Top-down DP with cache
dfs help find the the minimum difficulty
if start work at ith job with d days left.

If d = 1, only one day left, we have to do all jobs,
return the maximum difficulty of jobs.

```python
import functools
class Solution:
    def minDifficulty(self, A, d):
        n = len(A)
        if n < d: return -1

        @functools.lru_cache(None)
        def dfs(i, d):
            if d == 1:
                return max(A[i:])
            res, maxd = float('inf'), 0
            for j in range(i, n - d + 1):
                maxd = max(maxd, A[j])
                res = min(res, maxd + dfs(j + 1, d - 1))
            return res
        return dfs(0, d)

```

**Complexity Analysis**
TC:O(nnd)
SC:O(nd)
---
## Solution 2: Bottom-up 2D DP


```python
class Solution:
    def minDifficulty(self, A, d):
       n, inf = len(A), float('inf')
        dp = [[inf] * n + [0] for i in xrange(d + 1)]
        for d in xrange(1, d + 1):
            for i in xrange(n - d + 1):
                maxd = 0
                for j in xrange(i, n - d + 1):
                    maxd = max(maxd, A[j])
                    dp[d][i] = min(dp[d][i], maxd + dp[d - 1][j + 1])
        return dp[d][0] if dp[d][0] < inf else -1

```

**Complexity Analysis**
TC:O(nnd)
SC:O(nd)
---
## Solution 3: Bottom-up 1D DP


```python
class Solution:
    def minDifficulty(self, A, d):
       n, inf = len(A), float('inf')
        if n < d: return -1
        dp = [inf] * n + [0]
        for d in xrange(1, d + 1):
            for i in xrange(n - d + 1):
                maxd, dp[i] = 0, inf
                for j in xrange(i, n - d + 1):
                    maxd = max(maxd, A[j])
                    dp[i] = min(dp[i], maxd + dp[j + 1])
        return dp[0]

```

**Complexity Analysis**
TC:O(nnd)
SC:O(nd)
----

## Solution 4: Stack


```python
class Solution:
    def minDifficulty(self, A, d):
        n = len(A)
        if n < d: return -1
        dp, dp2 = [float('inf')] * n, [0] * n
        for d in xrange(d):
            stack = []
            for i in xrange(d, n):
                dp2[i] = dp[i - 1] + A[i] if i else A[i]
                while stack and A[stack[-1]] <= A[i]:
                    j = stack.pop()
                    dp2[i] = min(dp2[i], dp2[j] - A[j] + A[i])
                if stack:
                    dp2[i] = min(dp2[i], dp2[stack[-1]])
                stack.append(i)
            dp, dp2 = dp2, dp
        return dp[-1]

```

**Complexity Analysis**
TC:O(nd)
SC:O(n)