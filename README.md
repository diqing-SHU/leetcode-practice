# Leetcode Practice

Records all the questions and solutions while I am working through Leetcode

Some recommended questions can be found [here](https://github.com/diqing-SHU/leetcode-practice/blob/master/index.md)

For now the questions will be sorted by difficulty under different folders

---

#### 2021-04-18

Some useful Itertool functions:

`itertools.accumulate()`: information is [here](https://docs.python.org/3/library/itertools.html#itertools.accumulate). It's accumulate sum and return that array of accumulated sum

`itertools.combinations`: information is [here](https://docs.python.org/3/library/itertools.html#itertools.combinations). It generates combinations of that size and return the array. Combinations are sorted from small to large

---

#### 2021-04-26

Python heap queue (priority):

`heapq`: information is [here](https://docs.python.org/3/library/heapq.html). This implementation uses arrays for which heap[k] <= heap[2*k+1] and heap[k] <= heap[2*k+2] for all k, counting elements from zero. For the sake of comparison, non-existing elements are considered to be infinite. The interesting property of a heap is that its smallest element is always the root, heap[0].

---

#### 2021-04-29

I am constantly making mistake in writing binary search, here is a good template to follow:
```python
def search(target, lo, hi):
  while lo < hi:
    mid = (lo + hi) // 2
    if nums[mid] >= target:
      hi = mid
    else:
      lo = mid + 1
  return lo
```
One thing to keep in mind is that we are looking for first index to insert the target. Not just one index which has value == target
