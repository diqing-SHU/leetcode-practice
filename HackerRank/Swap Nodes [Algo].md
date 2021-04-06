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

My approach with recursion for in order traversal. notice that we need to increase recursion limits to pass large cases.

```python
#!/bin/python3

import os
import sys

# recrsion limit needs to be increase
# to pass last 2 cases
sys.setrecursionlimit(15000)

# define our tree structure
class TreeNode:
    def __init__(self, val):
        super().__init__()
        self.value = val
        self.left = None
        self.right = None

#
# Complete the swapNodes function below.
#
def swapNodes(indexes, queries):
    # helper to get in order traversal
    def getInorder(node):
        if node:
            return getInorder(node.left)+[node.value]+getInorder(node.right)
        return []
    # helper to swap nodes at certain level
    def swapNode(node, currLevel, k):
        if node:
            if currLevel%k == 0:
                # swap nodes here
                node.left, node.right = node.right, node.left
            # keep goind deep till we get to the leaves
            swapNode(node.left, currLevel+1, k)
            swapNode(node.right, currLevel+1, k)
    res = []
    print(indexes, queries)
    # build our tree first, using bfs
    root = TreeNode(1)
    currLevel, nextLevel = [root], []
    for (left, right) in indexes:
        if not currLevel:
            currLevel, nextLevel = nextLevel, []
        curr = currLevel.pop(0)
        if left != -1:
            curr.left = TreeNode(left)
            nextLevel.append(curr.left)
        if right != -1:
            curr.right = TreeNode(right)
            nextLevel.append(curr.right)
    # swap nodes on certain level
    for query in queries:
        # perform swap
        swapNode(root, 1, query)
        # add in-order travesal
        res.append(getInorder(root))
    return res

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input())

    indexes = []

    for _ in range(n):
        indexes.append(list(map(int, input().rstrip().split())))

    queries_count = int(input())

    queries = []

    for _ in range(queries_count):
        queries_item = int(input())
        queries.append(queries_item)

    result = swapNodes(indexes, queries)

    fptr.write('\n'.join([' '.join(map(str, x)) for x in result]))
    fptr.write('\n')

    fptr.close()
```
**Complexity Analysis**
TC:O(h) build tree, travel, and swap all have the time complexity up to height of the tree.
SC:O(n) need to build the tree for all elements.