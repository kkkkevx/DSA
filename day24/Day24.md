# Day 24: 代码随想录算法训练营

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
- 树层去重需要排序
- char convert to int:  use ASCII value `a = ch - '0';`

## LeetcodeProblem
[Recourse](https://programmercarl.com/0093.%E5%A4%8D%E5%8E%9FIP%E5%9C%B0%E5%9D%80.html#%E6%80%BB%E7%BB%93)

Leetcode 93
这道题很难 代码的细节很多 特别是在判断有效的IP上面

```java
class Solution {
    List<String> res = new ArrayList<>();
    public List<String> restoreIpAddresses(String s) {
        if (s.length() > 12) return res;
        StringBuilder path = new StringBuilder(s);
        backtracking(path, 0, 0);
        return res;
    }

    private void backtracking(StringBuilder sb, int startIdx, int pointNum) {
        if (pointNum == 3) {
            if (isValidIP(sb, startIdx, sb.length() - 1)) {
                res.add(sb.toString());
            }
            return;
        }

        for (int i = startIdx; i < sb.length(); i++) {
            if (!isValidIP(sb, startIdx, i)) break;
            sb.insert(i + 1, '.');
            backtracking(sb, i + 2, pointNum + 1);
            sb.deleteCharAt(i + 1);
        }
    }

    private boolean isValidIP (StringBuilder s, int start, int end) {
        if (start > end) return false;

        if (s.charAt(start) == '0' && start != end) return false; // when s has more than 1 integer, fisrt number can not be 0 

        int num = 0;
        for (int i = start; i <= end; i++) {
            if (s.charAt(i) < '0' || s.charAt(i) > '9') return false; //illegal char

            num = num * 10 + (s.charAt(i) - '0');
        }

        if (num > 255) return false;
        return true; 
    }
}
```

Leetcode 78
```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> subsets(int[] nums) {
        // 这道题不用排序 只需要遍历树的结构
        res.add(new ArrayList());
        backtracking(nums, 0);
        return res;
    }

    private void backtracking(int[] nums, int start) {
        if (start > nums.length) return;

        for (int i = start; i < nums.length; i++) {
            path.add(nums[i]);
            res.add(new ArrayList(path));
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }

    }
}
```

Leetcode 90 
```java
class Solution {
    /**
    树层去重需要排序
     */
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new ArrayList<>();
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        res.add(new ArrayList());
        Arrays.sort(nums);
        backtracking(nums, 0);
        return res;
    }

    private void backtracking(int[] nums, int start) {
        if (start >= nums.length) return;

        for (int i = start; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) continue; // 树层去重
            path.add(nums[i]);
            res.add(new ArrayList(path));
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```
