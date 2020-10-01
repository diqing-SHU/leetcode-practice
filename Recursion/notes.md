
----------

## D&C Template

----------

In the previous article of merge sort, we have introduced the general steps involved in all the divide-and-conquer algorithms. In this article, we will present you a  _**pseudocode**_  **_template_**  that could help you to structure your code when implementing the algorithm in the divide-and-conquer paradigm. Furthermore, we will demonstrate with some concrete examples on how to apply the template.

### Template

----------

There are in general three steps that one can follow in order to solve the problem in a divide-and-conquer manner.

> 1. **Divide.** Divide the problem  {S}S into a set of subproblems:  \{S_1, S_2, ... S_n\}{S1​,S2​,...Sn​} where  {n \geq 2}n≥2,  _i.e._  there are usually more than one subproblem.
> 
> 2.  **Conquer.** Solve each subproblem recursively.
> 
> 3. **Combine.** Combine the results of each subproblem.

We can summarize the above steps in the following pseudocode template.

As one can see from the above template, the essential part of the divide and conquer is to figure out the  `recurrence relationship`  between the subproblems and the original problem, which subsequently defines the functions of  `divide()`  and  `combine()`.

In the next sections, we will show you how to apply the above template to implement the algorithms for some concrete examples.

### Validate Binary Search Tree

----------

Sometimes, tree related problems can be solved using divide-and-conquer algorithms.

For example, look at the following problem statement:

> Given a binary tree, validate if the given tree is a binary search tree (BST). The BST must meet all of the following properties:
> 
> 1.  All values on the left subtree of a node should be less than the value of the node.
> 2.  All values on the right subtree of a node should be greater than the value of the node.
> 3.  Both the left and right subtrees must also be binary search trees.

Read  **point no. 3** above very carefully. The definition of BST is recursive in nature, making this a natural divide and conquer problem.

Below is an example of a BST shown in the following figure.

![](https://assets.leetcode.com/uploads/2019/03/31/bst_dac.png)

_Fig 2. Binary Search Tree_

> **1.**  In the first step, we divide the tree into two subtrees -- its left child and right child. (**Divide**)
> 
> **2.**  Then in the next step, we  _**recursively**_  validate each subtree is indeed a binary search tree. (**Conquer**)
> 
> **3.**  Upon the results of the subproblems from Step 2, we return true if and only if both subtrees are both valid BST. (**Combine**)

The recursion in  **Step 2.** would reach the base case where the subtree is either empty or contains a single node, which is a valid BST itself.

Notice some important details are still missing from **Step 2.** above, which are left as an exercise for the reader. For example, how do you verify these two properties which are also required for a BST?

> 1.  All values on the left subtree of a node should be less than the value of the node.
> 2.  All values on the right subtree of a node should be greater than the value of the node.

Following this article you can [try solving this exercise](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2874/) by yourself. We also provide a  [step-by-step solution](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2875/)  if you are still stuck following the exercise.

### Search a 2D Matrix II

----------

> Write an efficient algorithm that searches for an integer value in an {[m \times n]}[m×n] matrix. This matrix has the following properties:
> 
> -   Integers in each row are sorted in ascending from left to right.
> -   Integers in each column are sorted in ascending from top to bottom.

There are several ways to solve the above problem. Here we give an overall idea to solve it in the divide-and-conquer manner.

As one might notice, given the matrix, if we divide it into some sub-matrices by cutting it either by row and/or column, the resulting matrices would still keep the above two properties of the original matrix. Given the above insight, here is how we can apply the template to solve the problem.

> _**1**_. We divide the matrix into 4 sub-matrices by choosing a pivot point based on a row and a column. (**Divide**)
> 
> _**2**_. Then we  _**recursively**_  look into each sub-matrix to search for the desired target. (**Conquer**)
> 
> _**3**_. If we find the target in either of the sub-matrices, we stop the search and return the result immediately. (**Combine**)

The base cases in the above recursion would be either the input matrix is empty or it contains only a single element. As a simple strategy, one can choose the  **_middle point_**  both on the row and column as the pivot points to divide the matrix.

Do we really need to look into each of the divided 4 sub-matrices? Notice that the smallest and the largest element of the input matrix is located in the top left and bottom right corner respectively, which also applies to each of the divided sub-matrices. In fact, we need to only look into 3 of the sub-matrices.

> 1.  If our target is equal to the pivot, we have found our target and immediately return the result.
> 2.  If our target is less than the pivot, we can discard the bottom-right sub-matrix. All elements in that region must be greater or equal than the pivot.
> 3.  If our target is greater than the pivot, we can discard the top-left sub-matrix. All elements in that region must be less than or equal than the pivot.

We have just finished the divide-and-conquer approach, now try to [code the solution](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2872/) yourself! As a follow up exercise, can you derive the time complexity? At the end of this chapter, we provide  [Master Theorem](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2871/)  as an alternative way to derive time complexity like this problem.

The above divide-and-conquer algorithm can still be further improved, which we will provide insights below.

> _**As an improvement to the above divide-and-conquer algorithm, we could devise a better strategy by choosing the pivot points wisely.**_

We illustrate a strategy in the following figure, to reduce the search zones into 2 sub-matrices, instead of 3 sub-matrices.

![](https://assets.leetcode.com/uploads/2019/03/31/search_2d_matrix.png)

_Fig 1. Search 2D Matrix II_

First, we choose the middle point on the column which divides the matrix into two sub-matrices. We then fix on this middle column to further determine an optimal row to divide the matrix. We scan the elements along the chosen middle column, to locate the boundary where the value of the element just goes beyond the target value,  _i.e._ \{ V_{i-1} < \text{target} < V_i\}{Vi−1​<target<Vi​}. From this point, we divide the original matrix into 4 sub-matrices. And we just need to zoom into the bottom left and top right sub-matrices to look for the target value, while ignoring the top left and bottom right sub-matrices.

We ignore the top left sub-matrix that ends with the element  {V_{i-1}}Vi−1​, because all the elements within this sub-matrix would be less than the target value. Similarly, we ignore the bottom right sub-matrices that starts with the element  {V_i}Vi​, because we know that all the elements within this sub-matrix would be greater than the target value.

---

## Backtracking Template

----------

In this article, we will present you a pseudocode template that summarizes some common patterns for the backtracking algorithms. Furthermore, we will demonstrate with some concrete examples on how to apply the template.

### Template

----------

With the N-queen example as we presented in the previous article, one might have noticed some patterns about the backtracking algorithm. In the following, we present you a pseudocode template, which could help you to clarify the idea and structure the code when implementing the backtracking algorithms.
```python
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```
Here are a few notes about the above pseudocode.

-   Overall, the enumeration of candidates is done in two levels: 1). at the first level, the function is implemented as recursion. At each occurrence of recursion, the function is one step further to the final solution. 2). as the second level, within the recursion, we have an iteration that allows us to explore all the candidates that are of the same progress to the final solution.
  
-   The backtracking should happen at the level of the iteration within the recursion.
  
-   Unlike brute-force search, in backtracking algorithms we are often able to determine if a partial solution candidate is worth exploring further (_i.e._ `is_valid(next_candidate)`), which allows us to prune the search zones. This is also known as the constraint,  _e.g._  the attacking zone of queen in N-queen game.
  
-   There are two symmetric functions that allow us to mark the decision (`place(candidate)`) and revert the decision (`remove(candidate)`).

In the next sections, we show some concrete examples and explain how to apply the above pseudocode template.

### Robot Room Cleaner

----------

> Given a room that is represented as a grid of cells, where each cell contains a value that indicates whether it is an obstacle or not, we are asked to clean the room with a robot cleaner which can turn in four directions and move one step at a time.

This is a typical problem that can be solved with the backtracking paradigm, as many of you might have figured out from the description of the problem.

Before diving into the algorithm, to facilitate the explanation, we plot a figure below with the grid of room and the movements of robot. As one can see, the robot is denoted as the  `red`  dot and each step that the robot takes is marked as a footprint.

![](https://assets.leetcode.com/uploads/2019/04/06/robot_room_cleaner.png)

_Fig 1. Robot Room Cleaner_

We give the general idea below on how one can apply the above pseudocode template to implement a backtracking algorithm.

- [1]. One can model each step of the robot as a recursive function (_i.e._  `backtrack()`).

- [2]. At each step, technically the robot would have four candidates of direction to explore,  _e.g._  the robot located at the coordinate of  `(0, 0)`. Since not each direction is available though, one should check if the cell in the given direction is an obstacle or it has been cleaned before,  _i.e._  `is_valid(candidate)`. Another benefit of the check is that it would greatly reduce the number of possible paths that one needs to explore.

- [3]. Once the robot decides to explore the cell in certain direction, the robot should mark its decision (_i.e._  `place(candidate)`). More importantly, later the robot should be able to revert the previous decision (_i.e._  `remove(candidate)`), by going back to the cell and restore its original direction.

- [4]. The robot conducts the cleaning step by step, in the form of recursion of the  `backtrack()` function. The backtracking would be triggered whenever the robot reaches a point that it is surrounded either by the obstacles (_e.g._  cell at the row  `1`  and the column  `-3`) or the cleaned cells. At the end of the backtracking, the robot would get back to the its starting point, and each cell in the grid would be traversed at least once. As a result, the room is cleaned at the end.

### Sudoku Solver

----------

> Sudoku is a popular game that many of you are familiar with. The main idea of the game is to fill a grid with only the numbers from 1 to 9, while ensuring that each row and each column as well as each sub-grid of 9 elements does not contain duplicate numbers.

![](https://assets.leetcode.com/uploads/2019/03/31/sudoku_solver.png)

_Fig 2. Sudoku Game_

Once again, from the description of the Sudoku problem, one might have noticed the characteristics that hint on the solution of backtracking, such as the recursive nature of problem, a number of candidate solutions and some rules to filter out the candidates  _etc_.

Indeed, we could solve the problem with the paradigm of backtracking. We break down on how to apply the backtracking template to implement a sudoku solver in the following.

- [1]. Given a grid with some pre-filled numbers, the task is to fill the empty cells with the numbers that meet the constraint of Sudoku game. We could model the each step to fill an empty cell as a recursion function (_i.e._  our famous  `backtrack()`  function).

- [2]. At each step, technically we have 9 candidates at hand to fill the empty cell. Yet, we could filter out the candidates by examining if they meet the rules of the Sudoku game, (_i.e._  `is_valid(candidate)`).

- [3]. Then, among all the suitable candidates, we can try out one by one by filling the cell (i.e.  `place(candidate)`). Later we can revert our decision (_i.e._  `remove(candidate)`), so that we could try out the other candidates.

- [4]. The solver would carry on one step after another, in the form of recursion by the  `backtrack`  function. The backtracking would be triggered at the points where either the solver cannot find any suitable candidate (as shown in the above figure), or the solver finds a solution to the problem. At the end of the backtracking, we would enumerate all the possible solutions to the Sudoku game.