# Day 23: 代码随想录算法训练营

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
- Probblem 131  分割和组合抽象概念是一样的
- 当写完回溯后 尽力去剪枝

## Leetcode Problem
[Recourse](https://programmercarl.com/0039.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.html#%E6%80%BB%E7%BB%93)

Leetcode 39
```java
class Solution {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // Arrays.sort(candidates);
        backtracking(candidates, target, 0, 0);
        return res;
    }

    private void backtracking(int[] candidates, int target, int curSum, int startIndex) {
        if (curSum > target) return; //如果超过这个数就没有必要执行当前的loop了 要写在loop里 break 修枝首先要排序
        if (curSum == target) {
            res.add(new ArrayList(path));
            return;
        }

        for (int i = startIndex; i < candidates.length; i++) {
            curSum += candidates[i];
            path.add(candidates[i]);
            backtracking(candidates, target, curSum, i); // 不用i+1了，表示可以重复读取当前的数
            curSum -= candidates[i];
            path.remove(path.size() - 1);
        }
    }
}
```

Leetcode 40
第一感觉是用map或者set去重 但是时间超时
只能在递归中去重 树层去重就省去了重复做一样的事情 但是要先排序
```java
class Solution {
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        backtracking(candidates, target, 0, 0);
        return res;
    }

    private void backtracking(int[] candidates, int target, int sum, int idx) {
        if (sum == target) {
            res.add(new ArrayList(path));
            return;
        }

        for (int i = idx; i < candidates.length; i++) {
            if (sum + candidates[i] > target) break; // 去重 当target超过时没有必要去往下递归了。
            if (i > idx && candidates[i] == candidates[i-1]) continue; //树层去重
            sum += candidates[i];
            path.add(candidates[i]);
            backtracking(candidates, target, sum, i + 1);
            sum -= candidates[i];
            path.remove(path.size() - 1);
        }
    }
}
```

Leetcode 131
重点复习
```java
class Solution {
    List<List<String>> res = new ArrayList<>();
    List<String> path = new ArrayList<>();
    public List<List<String>> partition(String s) {

        backtraking(s, 0);
        return res;
    }

    private void backtraking(String s, int idx) {
        //如果起始位置大于s的大小，说明找到了一组分割方案        
        if (idx >= s.length()) {
            res.add(new ArrayList(path));
            return;
        }

        for (int i = idx; i < s.length(); i++) {
            if (isPalindrome(s, idx, i)) {
                String str = s.substring(idx, i + 1);
                path.add(str);
            } else {
                continue; // 不是回文就跳过
            }
            backtraking(s, i + 1);
            path.remove(path.size() - 1);
        }
    }

    private boolean isPalindrome(String s, int l, int r) {
        for (; l < r; l++, r--) {
            if (s.charAt(l) != s.charAt(r)) return false;
        }
        return true;
    }
}
```
