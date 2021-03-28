# Maximum Bounded Array

## Question

[Question link](https://aonecode.com/interview-question/maximum-bounded-array)

## Solution



```python
def MaxBoundedArray(n, low, up):
  maxLength = (up-low)*2+1
  # check if its possible
  if n > maxLength or up < low or n < 3:
    return None
  # if above check is passed, there definitely exists a solution
	q = collections.deque()
	# create the decreasing part
	for ele in range(up, low-1, -1):
		q.append(ele)
	# case 1: decreasing part has length >= n
	if len(q) >= n:
		while len(q) > n-1:
			q.pop()
		q.appendleft(up-1)
		return list(q)
	# case 2: decreasing part has length < n, so now we can just append left elements
	else:
		for ele in range(up-1, low-1, -1):
			q.appendleft(ele)
			if len(q) == n:
				return list(q)

```

**Complexity Analysis**
TC:O(n) need to build output array
SC:O(1) constant extra space
