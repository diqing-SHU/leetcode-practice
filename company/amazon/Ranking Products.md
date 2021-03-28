# Ranking Products

## Question

[Question link](https://aonecode.com/interview-question/ranking-products)

## Solution



```python
def fetch_results_to_display(sort_column, sort_order, results_per_page, page_index, results) :
 ordered = [(name, rel, price) for name, (rel, price) in results.items()]
 return []

 ordered.sort(key=lambda x: x[sort_column], reverse=sort_order == 1) 
 start_index = results_per_page * page_index 
 return [name for name, _, _ in ordered[start_index:start_index + results_per_page]]

```

**Complexity Analysis**
TC:O(nlogn) used built in sort
SC:O(n) extra dict used
