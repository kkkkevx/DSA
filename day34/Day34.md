# Day 34: 代码随想录算法训练营

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
- 当公式里面需要另一个变量的时候 我就很难理解 需要多加油 多做这种题 提高思路

## Leetcode Problem
[Recourse](https://programmercarl.com/0343.%E6%95%B4%E6%95%B0%E6%8B%86%E5%88%86.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)

leetcode 343
dp[i]：分拆数字i，可以得到的最大乘积为dp[i]。

`dp[i] = max(dp[i], max(j*dp[i-j], j*(i-j)))`
```java
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n + 1];
        dp[2] = 1;
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j <= i - j; j++) {
                dp[i] = Math.max(dp[i], Math.max(j * dp[i-j], j * (i - j)));
            }
        } 
        return dp[n];
    }
}
```

leetcode 96
```java
class Solution {
    public int numTrees(int n) {
        // i 有几个节点 dp[i] 有i个节点时有多少个组合
        // do[i] += dp[j-1] + dp[i-j];

        int[] dp = new int[n + 1];
        dp[0] = 1;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                dp[i] += dp[j - 1] * dp[i - j]; 
            }
        }

        return dp[n];
    }
}
```
