# Swap Nodes [Algo]

  
  

## Question:

[Question link](https://www.hackerrank.com/challenges/swap-nodes-algo/problem?isFullScreen=true)

  
  

## Solution:

Don't hesitate to create tree structure. You will need a structure to travel the tree after you made any changes/swaps

  

```python

#!/bin/python3

import os
import sys
# Build tree first
class Node:
	def __init__(self, val):
		self.val = val
		self.left = None
		self.right = None

#
# Complete the swapNodes function below.
#
def swapNodes(indexes, queries):
	#
	# Write your code here.
	#

	root = Node(1)
	queue = [root]
	# Build Binary Tree
	iIter = iter(indexes)
	while len(queue) > 0:
		cur = queue.pop(0)
		elem = next(iIter, None)
		if elem is  None:
			break
		left, right = elem
		if left != -1:
			cur.left = Node(left)
			queue.append(cur.left)
		if right != -1:
			cur.right = Node(right)
			queue.append(cur.right)

	def inorder(node, output):
		stack = [node]
		while  len(stack) > 0:
			cur = stack[-1]
			if cur.left is  not  None  and  not cur.left.val in output:
				stack.append(cur.left)
				continue
			cur = stack.pop(-1)
			output.append(cur.val)
			if cur.right is  not  None  and  not cur.right.val in output:
				stack.append(cur.right)
	
	# Start BFS
	res = []
	for query in queries:
	queue = [(1, root)]
	while  len(queue) > 0:
		curLevel, curNode = queue.pop(0)
		if curLevel % query == 0:
			# Swap
			curNode.right, curNode.left = curNode.left, curNode.right
		if curNode.left is  not  None:
			queue.append((curLevel + 1, curNode.left))
		if curNode.right is  not  None:
			queue.append((curLevel + 1, curNode.right))
			
	# Snapshot by dong inorder traversal
	output = []
	inorder(root, output)
	res.append(output)
	return res

```
**Complexity Analysis**
TC:O(h) build tree, travel, and swap all have the time complexity up to height of the tree.
SC:O(n) need to build the tree for all elements.