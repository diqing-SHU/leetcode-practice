# Leetcode Practice

Records all the questions and solutions while I am working through Leetcode

Some recommended questions can be found [here](https://github.com/diqing-SHU/leetcode-practice/blob/master/index.md)

For now the questions will be sorted by difficulty under different folders

---

## 2021-05-10

A common algorithm to generate prime numbers: [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

The general idea is to mark all multiples of a non-prime in a dictionary until we reach `sqrt(n)`. Then unmarked numbers are the prime numbers.

---

## 2021-05-28

Bitmask is a good approach to do comparison based on bits. Main idea is use `&` on two binary numbers (can be representation of string), result of 0 indicates that there is no overlaps.

More details on this [Sieve of Eratosthenes](https://dev.to/somedood/bitmasks-a-very-esoteric-and-impractical-way-of-managing-booleans-1hlf)

---