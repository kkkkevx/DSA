# Day 36: 代码随想录算法训练营 补

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
- 要多回来看看 继续体会01背包的思想 和看透这个问题

## Leetcode Problem
[Recourse](https://programmercarl.com/0474.%E4%B8%80%E5%92%8C%E9%9B%B6.html#%E6%80%9D%E8%B7%AF)

leetcode 1049

```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        // 找到最平均的两堆 然后消灭 是最小重量

        // dp[j] 当背包只有一半容量时最大能装多少（其中一堆）  target = sum / 2
        int sum = 0;
        for (int stone : stones) {
            sum += stone;
        }

        int target = sum / 2;

        int[] dp = new int[target + 1];

        for (int i = 0; i < stones.length; i++) {
            for (int j = target; j >= stones[i]; j--) {
                dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
            }
        }

        return sum - dp[target] - dp[target];
    }
}
```

leetcode 494

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        // sum(P) + sum(N) + sum(P) - sum(N) = 2 * sum(P) = sum(nums) + S
        // sum(P) = (sum(nums) + S)  / 2
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        if ((sum + target) % 2 != 0) return 0;
        if (Math.abs(target) > sum) return 0;
        int bagSize = (sum + target) / 2;
        int[] dp = new int[bagSize + 1];
        dp[0] = 1;

        for (int i = 0; i < nums.length; i++) {
            for (int j = bagSize; j >= nums[i]; j--) {
                dp[j] += dp[j - nums[i]];
            }
        }

        return dp[bagSize];
    }
}
```

leetcode 474

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        // dp[][] means i 0s j 1s 最大子集 
        int[][] dp = new int[m+1][n+1];
        int oneNum, zeroNum;

        for (String str : strs) {
            oneNum = 0;
            zeroNum = 0;
            for (char ch : str.toCharArray()) {
                if (ch == '0') {
                    zeroNum++;
                } else {
                    oneNum++;
                }
            }

            for (int i = m; i >= zeroNum; i--) {
                for (int j = n; j >= oneNum; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zeroNum][j - oneNum] + 1);
                }
            }
        }

        return dp[m][n];
    }
}
```
