# Robot Bounded In Circle

## Question

[Question link](https://leetcode.com/problems/robot-bounded-in-circle/)

## Solution
Starting at the origin and face north (0,1),
after one sequence of instructions,

- if robot return to the origin, he is obvious in an circle.
- if robot finishes with face not towards north, it will get back to the initial status in another one or three sequences.

```python
class Solution:
    def isRobotBounded(self, instructions: str) -> bool:
        x, y, dx, dy = 0, 0, 0, 1
        for i in instructions:
            if i == 'R': dx, dy = dy, -dx
            if i == 'L': dx, dy = -dy, dx
            if i == 'G': x, y = x + dx, y + dy
        return (x, y) == (0, 0) or (dx, dy) != (0,1)
```

**Complexity Analysis**
TC:O(n) one pass all instructions
SC:O(1) constant extra space
