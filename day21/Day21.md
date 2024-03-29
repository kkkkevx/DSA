# Day 21: 代码随想录算法训练营

## Topic:
- Backtracing


## Summary:
- backtracing algo is a way to find out all the combination or permuation
- template for backtracing
```
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```
- Java cannot directly add an array to a collection, such as with res.add(path), because it passes a reference, not the array itself. Therefore, using new ArrayList<>(Arrays.asList(path)) is a good way to pass every value.
- 
## Leetcode

Leetcode 77
```java
class Solution {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    List<Integer> path = new ArrayList<>();

    public List<List<Integer>> combine(int n, int k) {
        backtracking(1, n, k);
        return res;
    }

    private void backtracking(int start, int n, int k) {
        if (path.size() == k) {
            res.add(new ArrayList<>(path));
            return;
        }
        // 修枝 当n不足的时候就不往下挖了
        for (int i = start; i <= n - k + path.size() + 1; i++) {
            path.add(i);
            backtracking(i + 1, n, k);
            path.remove(path.size()-1);
        }
    }
}
```
