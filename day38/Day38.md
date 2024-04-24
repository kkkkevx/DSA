# Day 38: 代码随想录算法训练营 补

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
 
## Leetcode Problem

leetcode 322

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        // 如果目标金额为0，则无需硬币，返回0
        if (amount == 0) return 0;
        
        // 初始化二维dp数组，dp[i][j]表示使用前i种硬币凑出金额j所需的最少硬币数
        int[][] dp = new int[coins.length][amount + 1];

        // 第一行初始化：凑出金额为0则不需要硬币
        for (int i = 0; i < coins.length; i++) {
            dp[i][0] = 0;
        }
        
        // 第一列初始化：凑出其他金额至少需要一个硬币，或者占位符100000表示不可能达到
        for (int j = 1; j <= amount; j++) {
            if (j % coins[0] == 0) {
                dp[0][j] = j / coins[0];
            } else {
                dp[0][j] = 100000; // 占位符，表示不可能达到这个金额
            }
        }

        // 动态规划填表：状态转移方程为选择使用硬币i或不使用硬币i的最小值
        for (int i = 1; i < coins.length; i++) {
            for (int j = 1; j <= amount; j++) {
                if (j - coins[i] < 0) {
                    // 如果减去当前硬币面值后为负数，则无法使用该硬币
                    dp[i][j] = dp[i-1][j];
                } else {
                    // 选择使用硬币i或不使用硬币i的最小值
                    dp[i][j] = Math.min(dp[i-1][j], dp[i][j - coins[i]] + 1);
                }
            }
        }

        // 返回结果：如果无法凑出目标金额，则返回-1，否则返回最少硬币数
        return dp[coins.length - 1][amount] >= 100000 ? -1 : dp[coins.length - 1][amount];
    }
}
```

**一维**
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (amount == 0) return 0;

        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1); // 设定一个比目标金额大的初始值，代替占位符

        dp[0] = 0; // 目标金额为0时，所需硬币数为0

        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }
}
```
