# Leetcode Practice

Records all the questions and solutions while I am working through Leetcode

For now the questions will be sorted by difficulty under different folders

---

#### 2020-08-02

Half way through [Leetcode Binary Tree card questions](https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/). Its very helpful.

I decided to finish all the cards before moving on to random question in the future.

Notes will be taken for each of the topics for reviewing and referencing just in case.

---

#### 2020-08-03

Finished three more questions from [Leetcode Binary Tree card questions](https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/). Three more to go for tomorrow.

Some points can be summarized for the tree questions so far:
1. To construct binary tree from traversal:
	- We can use HashMap to reduce search time.
	- In recursion function, we only need to pass in the indexes for both traversal list and the length of current part. We can calculate the rest to reduce memory usage.
2. We can travel through tree backwards if needed (right to left)
3. DFS recursion approach is very useful:
	- With level as a parameter, we can achieve BFS.
	- Switch the order of (left sub tree call, right sub tree call and root return), we can achieve different traversal.

---

#### 2020-08-04

Finished remaining questions from [Leetcode Binary Tree card questions](https://leetcode.com/explore/learn/card/data-structure-tree/133/conclusion/). Today's questions are quite hard

Some Takeaways:

1. We can use iter to reduce time of get(i), which could take O(n) for some structure. But iterator's next is always O(1)

2. For back trace in binary trees, we can use postorder traverse. With flag to indicate whether we reach our target node yet.
	- For example: [236.Lowest Common Ancestor of a Binary Tree](https://leetcode.com/articles/lowest-common-ancestor-of-a-binary-tree/#)
3. Bit mask can be used to filter out results:
	- Like power of 4 in all 32 bit. we can XOR all possible results to generate a bit mask for it
4. A special trick to generate all possible binary bitmasks of length n:
```python
# Take value from take all binary string from 2^n to 2^(n+1).
# Then remove first 3 (0b1).
# The rest are all the possible binary bitmasks with leading 0s
# (if we take 0 to 2^n, we need to worry about it)
for i in range(2**n, 2**(n + 1)):
	# generate bitmask, from 0..00 to 1..11
	bitmask = bin(i)[3:]
```

---

#### 2020-08-05


Started to work on array questions from [Array Questions](https://leetcode.com/explore/featured/card/fun-with-arrays/521/introduction/). But today is mainly spent on Trie questions. Definitely needs more practice on it since I never learnt it before.


Some Takeaways:

1. [any()](https://www.w3schools.com/python/ref_func_any.asp) function is quite useful. Along with [all()](https://www.w3schools.com/python/ref_func_all.asp). Learn to use them!

2. For back trace in binary trees, we can:
	- Use postorder traverse and pass along a parameter path with it. if `root == node or left or right`, we return True and append node to path. Have to DFS so order is reversed for path
3. Trie structure basically has a children attribute which is a dict of same class (much like tree)
4. Use `{}` is better than `dict()`, same with `[]`
5. An is_end attribute can simply our code in trie
6. `defaultdict` from `collections` allows dict to have default `None` keys and values so we don't need to check when adding. Use it when allows
```python
from collections import defaultdict
    
def _trie():
    return defaultdict(_trie)
```

---
  

#### 2020-08-06

  

About half way on array questions from [Array Questions](https://leetcode.com/explore/featured/card/fun-with-arrays/521/introduction/). Today's challenge is also an array question (442)


Some Takeaways:

1. 2 pointers is very useful in array
2. Python `sort()`  uses a special version of merge sort, called Timsort, which runs in  **nlog2n**  time. So if we can have **O(n)** solution, don't use it.
3. If an array hold unique values, we can use it as a hash map:
	- For example:  [442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/discuss/775738/Python-2-solutions-with-O%28n%29-timeO%281%29-space-explained)

---
  

#### 2020-08-07

  

Three questions left from [Array Questions](https://leetcode.com/explore/featured/card/fun-with-arrays/521/introduction/). Today's challenge is a tree question (987). The concept is not hard. But the amount of code to construct is crazy. I am too tired to find out my solution missed on the sorting part. Will come back to it afterwards.


Some Takeaways:

1. Some useful code for sort dictionary with keys or value:
```python
# sort with key
for key in sorted(mydict.keys()):
    print("%s: %s" % (key, mydict[key]))
# sort with value
for key, value in sorted(mydict.items(), key=lambda item: item[1]):
    print("%s: %s" % (key, value))
```
2. Move element by condition in array, we can do it one pass in-place:
```python
class Solution:
    def sortArrayByParity(self, A: List[int]) -> List[int]:
        j = 0
        for i in range(len(A)):
            if A[i]%2 == 0:
                A[i], A[j] = A[j], A[i]
                j+=1
        return A
```