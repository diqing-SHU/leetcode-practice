# Notes on tree questions

## Traverse a Tree
### Pre-order Traversal

----------

Pre-order traversal is to visit the root first. Then traverse the left subtree. Finally, traverse the right subtree. 

### In-order Traversal

----------

In-order traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree.

Typically, for `binary search tree`, we can retrieve all the data in sorted order using in-order traversal. 



### Post-order Traversal

----------

Post-order traversal is to traverse the left subtree first. Then traverse the right subtree. Finally, visit the root.

Here is an animation to help you understand post-order traversal:

It is worth noting that when you delete nodes in a tree, deletion process will be in post-order. That is to say, when you delete a node, you will delete its left child and its right child before you delete the node itself.

Also, post-order is widely use in mathematical expression. It is easier to write a program to parse a post-order expression. Here is an example:

![](https://leetcode.com/explore/learn/card/data-structure-tree/134/traverse-a-tree/Figures/binary_tree/mathematical_expression.png)

You can easily figure out the original expression using the inorder traversal. However, it is not easy for a program to handle this expression since you have to check the priorities of operations.

If you handle this tree in postorder, you can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.
## Level-order Traversal
Level-order traversal is to traverse the tree level by level.

`Breadth-First Search`  is an algorithm to traverse or search in data structures like a tree or a graph. The algorithm starts with a root node and visit the node itself first. Then traverse its neighbors, traverse its second level neighbors, traverse its third level neighbors, so on and so forth.

When we do breadth-first search in a tree, the order of the nodes we visited is in level order.

Typically, we use a queue to help us to do BFS. 

---

## Solve Tree Problems Recursively
Typically, we can solve a tree problem recursively using a top-down approach or using a bottom-up approach.

### "Top-down" Solution

----------

"Top-down" means that in each recursive call, we will visit the node first to come up with some values, and pass these values to its children when calling the function recursively. So the "top-down" solution can be considered as a kind of **preorder** traversal. To be specific, the recursive function `top_down(root, params)` works like this:

1. return specific value for null node
2. update the answer if needed                      // answer <-- params
3. left_ans = top_down(root.left, left_params)      // left_params <-- root.val, params
4. right_ans = top_down(root.right, right_params)   // right_params <-- root.val, params 
5. return the answer if needed                      // answer <-- left_ans, right_ans

For instance, consider this problem: given a binary tree, find its maximum depth.

We know that the depth of the root node is  `1`. For each node, if we know its depth, we will know the depth of its children. Therefore, if we pass the depth of the node as a parameter when calling the function recursively, all the nodes will know their depth. And for leaf nodes, we can use the depth to update the final answer. Here is the pseudocode for the recursive function  `maximum_depth(root, depth)`:

1. return if root is null
2. if root is a leaf node:
3.      answer = max(answer, depth)         // update the answer if needed
4. maximum_depth(root.left, depth + 1)      // call the function recursively for left child
5. maximum_depth(root.right, depth + 1)     // call the function recursively for right child


### "Bottom-up" Solution

----------

"Bottom-up" is another recursive solution. In each recursive call, we will firstly call the function recursively for all the children nodes and then come up with the answer according to the returned values and the value of the current node itself. This process can be regarded as a kind of  **postorder**  traversal. Typically, a "bottom-up" recursive function  `bottom_up(root)`  will be something like this:

1. return specific value for null node
2. left_ans = bottom_up(root.left)          // call function recursively for left child
3. right_ans = bottom_up(root.right)        // call function recursively for right child
4. return answers                           // answer <-- left_ans, right_ans, root.val

Let's go on discussing the question about maximum depth but using a different way of thinking: for a single node of the tree, what will be the maximum depth  `x`  of the subtree rooted at itself?

If we know the maximum depth  `l`  of the subtree rooted at its  **left**  child and the maximum depth  `r`  of the subtree rooted at its  **right**  child, can we answer the previous question? Of course yes, we can choose the maximum between them and add 1 to get the maximum depth of the subtree rooted at the current node. That is  `x = max(l, r) + 1`.

It means that for each node, we can get the answer after solving the problem for its children. Therefore, we can solve this problem using a "bottom-up" solution. Here is the pseudocode for the recursive function  `maximum_depth(root)`:

1. return 0 if root is null                 // return 0 for null node
2. left_depth = maximum_depth(root.left)
3. right_depth = maximum_depth(root.right)
4. return max(left_depth, right_depth) + 1  // return depth of the subtree rooted at root

### Conclusion

----------

It is not easy to understand recursion and find out a recursive solution for the problem. It needs practice.

When you meet a tree problem, ask yourself two questions: Can you determine some parameters to help the node know its answer? Can you use these parameters and the value of the node itself to determine what should be the parameters passed to its children? If the answers are both yes, try to solve this problem using a "`top-down`" recursive solution.

Or, you can think of the problem in this way: for a node in a tree, if you know the answer of its children, can you calculate the answer of that node? If the answer is yes, solving the problem recursively using a  `bottom up`  approach might be a good idea.