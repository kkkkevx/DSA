# Day 40: 代码随想录算法训练营 补

## Topic:
- Dynamic Programming


## Summary:
- 动态规划中每一个状态一定是由上一个状态推导出来的
- DP五部曲
  - 确定dp数组（dp table）以及下标的含义 （！！！）
  - 确定递推公式 （！！！）
  - dp数组如何初始化
  - 确定遍历顺序
  - 举例推导dp数组

## Leetcode Probelm

leetcode 198
```java
class Solution {
    public int rob(int[] nums) {
        // dp[i]表示当偷到i间的时候 最多的收益
        // dp[i] = dp[i-2] + num[i] vs dp[i-1]

        // int[] dp = new int[nums.length + 1];
        // dp[0] = 0;
        // dp[1] = nums[0];

        // for (int i = 2; i <= nums.length; i++) {
        //     dp[i] = Math.max(dp[i - 1], dp[i-2] + nums[i - 1]);
        // }

        // return dp[nums.length];

        // 空间压缩
        int prev1 = 0; // dp[i-2]
        int prev2 = nums[0]; // dp[i-1]

        for (int i = 1; i < nums.length; i++) {
            int cur = Math.max(prev2, prev1 + nums[i]);
            prev1 = prev2;
            prev2 = cur;
        }

        return prev2;
    }
}
```

leetcode 213
```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        int res1 = helper(nums, 0, nums.length - 2);
        int res2 = helper(nums, 1, nums.length - 1);
        return Math.max(res1, res2);
    }

    private int helper (int[] nums, int start, int end) {
        int prev1 = 0; // dp[i-2]
        int prev2 = nums[start]; // dp[i-1]

        for (int i = start + 1; i <= end; i++) {
            int cur = Math.max(prev2, prev1 + nums[i]);
            prev1 = prev2;
            prev2 = cur;
        }

        return prev2;
    }
}
```

leetcode 337

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int rob(TreeNode root) {
        if (root == null) return 0;

        int money = root.val;
        if (root.left != null) {
            money += rob(root.left.left) + rob(root.left.right);
        }
        if (root.right != null) {
            money += rob(root.right.left) + rob(root.right.right);
        }

        return Math.max(money, rob(root.left) + rob(root.right));

    }
}
```
