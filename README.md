# Leetcode Practice

Records all the questions and solutions while I am working through Leetcode

Some recommended questions can be found [here](https://github.com/diqing-SHU/leetcode-practice/blob/master/index.md)

For now the questions will be sorted by difficulty under different folders

---

## 2021-06-05

Have some better understanding of heap usage now.

Found 2 functions that can help writing elegant Python code:

1. `zip`: `zip` two list together (length depends on shorter one). Link is [here](https://www.w3schools.com/python/ref_func_zip.asp)
2. `[::-1]`: add `[::-1]` after a list to reverse it

---

## 2021-06-09

Decreasing/increasing Deque is a good technique to use when you only care about min/max value after operation. It involves only keeping track of values that follows decreasing/increasing order in deque (or stack if deque is overkill)

Questions from easy to hard often utilize this technique. Examples are:

- `155. Min Stack`
- `1696. Jump Game VI`
- `239. Sliding Window Maximum`
