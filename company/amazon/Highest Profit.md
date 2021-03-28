# Highest Profit

## Question

[Question link](https://leetcode.com/discuss/interview-question/1092472/Amazon-or-OA-or-highest-profit)

## Solution


```python
def highestProfit(numSuppliers, inventory, order):
        # add [(0,0)] as when we sell all items
        # we are comparing with next one so we need the extra col
        arr = sorted(Counter(inventory).items(), reverse=True)+[(0,0)]
        print(arr)
        ans, ind, width = 0,0,0
        while order>0:
            # get the width of items we can sell at same price together
            width += arr[ind][1]
            # sell is the the number of items we sold in here
            # (arr[ind][0] - arr[ind+1][0]) is the height
            sell = min(order, width * (arr[ind][0] - arr[ind+1][0]))
            # if we didn't sell all (width * (arr[ind][0] - arr[ind+1][0])),
            # we need to check how many lines and remainder we have
            # to calculate our profit
            whole, remainder= divmod(sell, width)
            # calculate profit we made here
            ans += width*(whole*(arr[ind][0]+arr[ind][0]-(whole-1)))//2 + remainder*(arr[ind][0]-whole)
            # update order and index of col
            order -= sell
            ind += 1
        return ans 
```

**Complexity Analysis**
TC:O(nlogn) max time happened in sort
SC:O(n) sorted array of inventory is stored
