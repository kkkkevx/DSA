# Day 25: 代码随想录算法训练营

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
- 思考 为什么不能用path.remove(i-1) 因为在loop的时候 i不能准确表达当前path中最后一位
  - [1,2,3] 当 [1,2] 循环到[1,3]的时候 i=3 而path里面只是2个元素
- 回溯里面能大概画出树状图就能清楚看到解决方案， 细节上还需要多加练习

## Leetcode Problem:
[Recourse](https://programmercarl.com/0046.%E5%85%A8%E6%8E%92%E5%88%97.html#%E6%80%9D%E8%B7%AF)

Leetcode 491
```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> findSubsequences(int[] nums) {
        backtracking(nums, 0);
        return res;
    }

    private void backtracking(int[] nums, int start) {
        if (path.size() > 1) {
            res.add(new ArrayList(path));
        };

        Set<Integer> set = new HashSet<>();

        for (int i = start; i < nums.length; i++) {
            // 两个条件 1：后面的元素小 2： 树层重复 像4767 取了 47后 不应该取第二个47 （用set避免）
            if ((!path.isEmpty() && nums[i] < path.get(path.size() - 1)) || set.contains(nums[i])) continue; 
            set.add(nums[i]);
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

Leetcode 46
```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        boolean[] used = new boolean[nums.length];
        backtracking(nums, used);
        return res;
    }

    private void backtracking(int[] nums, boolean[] used) {
        if (path.size() == nums.length) {
            res.add(new ArrayList(path));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue;
            used[i] = true;
            path.add(nums[i]);
            backtracking(nums, used);
            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
}
```

Leetcode 47
```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> permuteUnique(int[] nums) {
        boolean[] used = new boolean[nums.length];
        Arrays.sort(nums);
        backtracking(nums, used);
        return res;
    }

    private void backtracking(int[] nums, boolean[] used) {
        if (path.size() == nums.length) {
            res.add(new ArrayList(path));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            // 树层去重 这里用到used[i-1]是同层 重复 当used[i-1] 是true时 说明在下一层
            if (i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false) continue;

            if (used[i] == false) {
                used[i] = true;
                path.add(nums[i]);
                backtracking(nums, used);
                path.remove(path.size() - 1);
                used[i] = false;
            }
        }
    }
}
```
