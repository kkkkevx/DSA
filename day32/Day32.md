# Day 31: 代码随想录算法训练营

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
[Recourse](https://programmercarl.com/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

Leetcode 509
i: 第i个斐波那契数组 dp[i] 第i个的值
dp[i] = dp[i-1] + dp[i-2]
```java
class Solution {
    public int fib(int n) {
        // recursive
        // if (n == 0) return 0;
        // if (n == 1) return 1;
        // return fib(n-1) + fib(n-2);

        // DP
        if (n <= 1) return n;
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

Leetcode 70
i: 第几层楼梯 dp[i]到i层有多少种可能
dp[i] = dp[i-1] + dp[i+2]
这里疑惑的点是 dp需要n+1 因为要算0层
```java
class Solution {
    public int climbStairs(int n) {
        if (n <=2 ) return n;
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }

        return dp[n];
    }
}
```

Leetcode 746
i: 第几层台阶 dp[i]： 到i层台阶需要多少cost
dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        // 楼梯顶层是cost.length + 1。 cost 的size不是顶层
        int[] dp = new int[cost.length+1];
        dp[0] = 0;
        dp[1] = 0;

        for (int i = 2; i <= cost.length; i++) {
            dp[i] = Math.min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]);
        }

        return dp[cost.length];
    }
}
```
