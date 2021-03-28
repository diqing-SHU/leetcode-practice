# Load The Cargo

  
  

## Question:

[Question link](https://aonecode.com/interview-question/load_cargo)

  
  

## Solution:

Not much

  

```python
def loadTheCargo(num: int, containers: List[int], itemSize: int, itemsPerContainer: List[int], cargoSize: int) -> int: 
    containerDict, res = {}, 0
    for i in range(num):
        if itemsPerContainer[i] not in containerDict:
            containerDict[itemsPerContainer[i]] = 0
        containerDict[itemsPerContainer[i]] += containers[i]

    for containerSize in sorted(containerDict.keys(),reverse=True):
        # cant load next level container
        if cargoSize <= containerDict[containerSize]:
            res+=containerSize*cargoSize
            return res
        res+=containerSize*containerDict[containerSize]
        cargoSize-=containerDict[containerSize]
    return res

```
**Complexity Analysis**
TC:O(nlogn) used sort on dict keys
SC:O(n) extra dict used