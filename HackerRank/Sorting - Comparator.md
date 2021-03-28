# Sorting: Comparator


## Question:

[Question link](https://www.hackerrank.com/challenges/ctci-comparator-sorting/problem?h_l=interview&playlist_slugs%5B%5D%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D%5B%5D=sorting&isFullScreen=true&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen)



## Solution:
Not much

```python
from functools import cmp_to_key
class Player:
    def __init__(self, name, score):
        self.name = name
        self.score = score
    def __repr__(self):
        return str(self.score)+self.name
    def comparator(a, b):
        if a.score < b.score:
            return 1
        elif a.score > b.score:
            return -1
        else:
            if a.name == b.name:
                return 0
            else:
                p = 0
                while p < len(a.name) and p < len(b.name):
                    if a.name[p] < b.name[p]:
                        return -1
                    elif a.name[p] > b.name[p]:
                        return 1
                    p+=1
                if p < len(a.name):
                    return 1
                if p < len(b.name):
                    return -1
n = int(input())
data = []
for i in range(n):
    name, score = input().split()
    score = int(score)
    player = Player(name, score)
    data.append(player)
    
data = sorted(data, key=cmp_to_key(Player.comparator))
for i in data:
    print(i.name, i.score)
```
**Complexity Analysis**
TC:O(n) max time is go over shortest word of a and b
SC:O(1) no extra space