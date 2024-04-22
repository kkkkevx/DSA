# Day 37: 代码随想录算法训练营 补

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
- 完全背包 每个物品可以无限拿
- 遍历会变的很重要 解决问题逻辑的体现
- 组合问题 的dp公式 dp[j] += dp[j - cost[i]]

## Leetcode Problem:

leetcode 518

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount+1];

        dp[0] = 1;

        for (int i = 0; i < coins.length; i++) {
            for (int j = coins[i]; j <= amount; j++) {
                dp[j] += dp[j - coins[i]];
            }
        }

        return dp[amount];
    }
}
```
2d 
```java
public static long countWays(int[] coins, int amount) {
		// base case 1
		if (amount == 0) return 1;

		// base case 2
		if (amount < 0) return 0;

		// create and initialize the 2-D array
		long dp[][] = new long[amount + 1][coins.length];
        for(long[] row:dp) {
            Arrays.fill(row, 1);
        }

		// iterate over the 2-D array and update the values accordingly
		for (int i = 1; i < amount + 1; i++) {
			for (int j = 0; j < coins.length; j++) {
				int coin = coins[j];
				int amt = i;
				long x = 0;
				long y = 0;

				// keep the count of solutions including coins[j]
				if (amt - coin >= 0) 
					x = dp[amt - coin][j];
				else
					x = 0;

				// keep the count of solutions excluding coins[j]
				if (j >= 1)
					y = dp[amt][j-1];
				else
					y = 0;

				dp[amt][j] = x + y;
			}
		}		
		return dp[amount][coins.length - 1];
	}
```
