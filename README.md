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