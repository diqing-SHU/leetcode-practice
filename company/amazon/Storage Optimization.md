# Storage Optimization

## Question

[Question link](https://algo.monster/problems/storage_optimization)

## Solution


```python
def storage_optimization(n: int, m: int, h: List[int], v: List[int]) -> int:
    # record the row/col to remove in dict
    # to reduce lookup time
    rowToRemove = Counter(h)
    colToRemove = Counter(v)
    rowMax, colMax, temp = 0, 0, 0
    # count and find the max row length and col length
    for row in range(1,n+1):
        if row not in rowToRemove:
            temp+=1
        else:
            rowMax, temp = max(rowMax, temp), 0
    for col in range(1, m+1):
        if col not in rowToRemove:
            temp+=1
        else:
            colMax, temp = max(colMax, temp), 0
    # get the max area (that largest one)           
    return colMax*rowMax
```

**Complexity Analysis**
TC:O(n) two pass to get colMax and rowMax
SC:O(n) used dict to store rowToRemove and colToRemove
