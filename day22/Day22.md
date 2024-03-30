# Day 22: 代码随想录算法训练营

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
- The time complexity of backtracking is often exponential, O(b^d), where "b" is the branching factor (number of choices at each decision point) and "d" is the depth of the recursion (the length of the solution or the number of decision points)
## Leetcode Problem
[Recourse](https://programmercarl.com/0216.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CIII.html)

Leetcode 216
```java
// class Solution {
//     private List<List<Integer>> res = new ArrayList<List<Integer>>();
//     private List<Integer> path = new ArrayList<>();
//     public List<List<Integer>> combinationSum3(int k, int n) {
//         backtracking(1, k, n);
//         return res;
//     }

//     private void backtracking(int start, int k, int n) {
//         if (path.size() == k) {
//             int sum = path.stream().reduce(0, Integer::sum);
//             if (sum == n) {
//                 res.add(new ArrayList<>(path));
//                 return;
//             } else {
//                 return;
//             }
//         }

//         for (int i = start; i <=9; i++) {
//             path.add(i);
//             backtracking(i + 1, k, n);
//             path.remove(path.size() - 1);
//         }
//     }
// }
class Solution {
	List<List<Integer>> result = new ArrayList<>();
	LinkedList<Integer> path = new LinkedList<>();

	public List<List<Integer>> combinationSum3(int k, int n) {
		backTracking(n, k, 1, 0);
		return result;
	}

	private void backTracking(int targetSum, int k, int startIndex, int sum) {
		// 减枝
		if (sum > targetSum) {
			return;
		}

		if (path.size() == k) {
			if (sum == targetSum) result.add(new ArrayList<>(path));
			return;
		}

		// 减枝 9 - (k - path.size()) + 1
		for (int i = startIndex; i <= 9 - (k - path.size()) + 1; i++) {
			path.add(i);
			sum += i;
			backTracking(targetSum, k, i + 1, sum);
			//回溯
			path.removeLast();
			//回溯
			sum -= i;
		}
	}
}
```

Leetcode 17
```java
class Solution {
    private List<String> res = new ArrayList<>();
    private String[] dict = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    private StringBuilder path = new StringBuilder();
    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0 || digits == null) return res;
        backtracking(digits, 0);
        return res;
    }

    private void backtracking(String digits, int index) {
        if (path.length() == digits.length()) {
            res.add(path.toString());
            return;
        }
        String str = dict[digits.charAt(index) - '0'];
        for (int i = 0; i < str.length(); i++) {
            path.append(str.charAt(i));
            backtracking(digits, index + 1);
            path.deleteCharAt(path.length() - 1);
        }
    }
}
```
