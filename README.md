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
2.	We can travel through tree backwards if needed (right to left)
3.	DFS recursion approach is very useful:
	- With level as a parameter, we can achieve BFS.
	- Switch the order of (left sub tree call, right sub tree call and root return), we can achieve different traversal.