# Shopping Options

## Question

[Question link](https://leetcode.com/discuss/interview-question/1110343/Amazon-OA-or-Experienced-developer)
It's basically [4SUM](https://leetcode.com/problems/4sum-ii/)

## Solution


```python
def recruitmentCombinations(productManagers, softwareEngineers, accountManagers, programManagers, budget):
    """
    :type productManagers: List[int]
    :type softwareEngineers: List[int]
    :type accountManagers: List[int]
    :type programManagers: List[int]
    :type budget: int
    :rtype: int
    """
    appearDict1, appearDict2, res = {}, {}, 0
    for pm in productManagers:
        for se in softwareEngineers:
            if pm+se not in appearDict1:
                appearDict1[pm+se] = 0
            appearDict1[pm+se]+=1
    for pm in programManagers:
        for am in accountManagers:
            if pm+am not in appearDict2:
                appearDict2[pm+am] = 0
            appearDict2[pm+am]+=1
    for val1 in appearDict1.keys():
        for val2 in appearDict2.keys():
            if val1+val2 <= budget:
                res+=appearDict1[val1]*appearDict2[val2]
    return res
```

**Complexity Analysis**
TC:O(n^2) 3 n^2 loop
SC:O(n^2) 2 n^2 HashMap
