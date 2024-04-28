# Day 41-43: 

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
- 今天是股票合集
- 状态转移公式是 dp[i][k][0/1]第i天 最多做k次操作0是卖1是买

## Leetcode Problem
[Recourse](https://labuladong.online/algo/dynamic-programming/stock-problem-summary/#%E4%B8%87%E6%B3%95%E5%BD%92%E4%B8%80)

leetcode 121
```java
class Solution {
    public int maxProfit(int[] prices) {
        //dp[i][k][0/1] 第i天最多k次交易 0是卖 1是买
        int n = prices.length;
        int[][][] dp = new int[n + 1][2][2];
        dp[0][1][0] = 0; // 没还开始
        dp[0][1][1] = Integer.MIN_VALUE; // 还没开盘你凭什么能卖了 你作弊
        dp[0][0][0] = 0; // 你不被允许交易
        dp[0][0][1] = Integer.MIN_VALUE; // 你想卖但是你不被允许卖

        for (int i = 1; i <= n; i++) {
            dp[i][1][0] = Math.max(dp[i-1][1][0], dp[i-1][1][1] + prices[i-1]);
            dp[i][1][1] = Math.max(dp[i-1][1][1], dp[i-1][0][0] - prices[i-1]);
        }
        return dp[n][1][0];

        // int n = prices.length;
        // int dp_i_0 = 0, dp_i_1 = Integer.MIN_VALUE;
        // for (int i = 0; i < n; i++) {
        //     dp_i_0 = Math.max(dp_i_0, dp_i_1 + prices[i]);
        //     dp_i_1 = Math.max(dp_i_1, -prices[i]);
        // }

        // return dp_i_0;
    }
}
```

leetcode 122
```java
class Solution {
    public int maxProfit(int[] prices) {
        // k没有必要
    //     int n = prices.length;
    //     int[][] dp = new int[n + 1][2];
    //     dp[0][0] = 0;
    //     dp[0][1] = Integer.MIN_VALUE;

    //     for (int i = 1; i <= n; i++) {
    //         dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1] + prices[i-1]); //卖
    //         dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0] - prices[i-1]); // 买
    //     }

    //     return dp[n][0];
        int n = prices.length;
        int dp_i_0 = 0, dp_i_1 = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++) {
            int temp = dp_i_0; // 要提前记录因为dp_i_0被更新了
            dp_i_0 = Math.max(dp_i_0, dp_i_1 + prices[i]);
            dp_i_1 = Math.max(dp_i_1, temp - prices[i]);
        }

        return dp_i_0;
    }
}
```

leetcode 123
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;

        int[][][] dp = new int[n + 1][3][2];

        // 初始化状态
        for (int i = 0; i <= n; i++) {
            dp[i][0][0] = 0;
            dp[i][0][1] = -prices[0];
        }

        for (int k = 0; k < 3; k++) {
            dp[0][k][0] = 0;
            dp[0][k][1] = -prices[0];
        }

        // 开始状态转移
        for (int i = 1; i <= n; i++) {
            for (int k = 2; k > 0; k--) {
                dp[i][k][0] = Math.max(dp[i-1][k][0], dp[i-1][k][1] + prices[i-1]);
                dp[i][k][1] = Math.max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i-1]);
            }
        }

        // 返回最后一天，完成两次交易且不持有股票时的最大利润
        return dp[n][2][0];
    }
}
```

leetcode 309
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n + 1][2];
        dp[0][0] = 0;
        dp[0][1] = Integer.MIN_VALUE;

        for (int i = 1; i <= n; i++) {
            if (i <= 1) { // 第一次交易不考虑冷冻期
                dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1] + prices[i-1]); //卖
                dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0] - prices[i-1]); // 买
            } else {
                dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1] + prices[i-1]); //卖
                dp[i][1] = Math.max(dp[i-1][1], dp[i-2][0] - prices[i-1]); // 买
            }    
        }

        return dp[n][0];
    }
}
```

leetcode 714
```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int n = prices.length;
        int[][] dp = new int[n + 1][2];
        dp[0][0] = 0;
        dp[0][1] = -prices[0];

        for (int i = 1; i <= n; i++) {
            dp[i][0] = Math.max(dp[i-1][0], dp[i-1][1] + prices[i-1] - fee); //卖
            dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0] - prices[i-1]); // 买
        }

        return dp[n][0];
    }
}
```

leetcode 188
```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;

        int[][][] dp = new int[n + 1][k + 1][2];

        // 初始化状态
        for (int i = 0; i <= n; i++) {
            dp[i][0][0] = 0;
            dp[i][0][1] = -prices[0];
        }

        for (int j = 0; j <= k; j++) {
            dp[0][j][0] = 0;
            dp[0][j][1] = -prices[0];
        }

        // 开始状态转移
        for (int i = 1; i <= n; i++) {
            for (int j = k; j > 0; j--) {
                dp[i][j][0] = Math.max(dp[i-1][j][0], dp[i-1][j][1] + prices[i-1]);
                dp[i][j][1] = Math.max(dp[i-1][j][1], dp[i-1][j-1][0] - prices[i-1]);
            }
        }

        // 返回最后一天，完成两次交易且不持有股票时的最大利润
        return dp[n][k][0];
    }
}
```
