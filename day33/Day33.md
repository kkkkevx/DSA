# Day 32: 代码随想录算法训练营

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
[Recourse](https://programmercarl.com/0062.%E4%B8%8D%E5%90%8C%E8%B7%AF%E5%BE%84.html)

leetcode 62
(i, j)location dp[i,j]到（i，j）有多少种方法
dp[i][j] = dp[i-1][j] + dp[i][j-1]
最左最右只有一种可能
```JAVA
class Solution {
    public int uniquePaths(int m, int n) {
        // O(m*n)
        // dp[i][j] = dp[i-1][j] + dp[i][j-1]
        int[][] dp = new int[m][n];
        dp[0][0] = 1; // start
        // 最高那一排只有一种可能
        // 最左边那一排也只有一种可能
        // 这样避免了溢出的可能
        for (int i = 1; i < n; i++) {
            dp[0][i] = 1;
        }
        for (int i = 1; i < m; i++) {
            dp[i][0] = 1;
        }
        for (int row = 1; row < m; row++) {
            for (int column = 1; column < n; column++) {

                dp[row][column] = dp[row][column - 1] + dp[row - 1][column];
            }
        }

        return dp[m - 1][n - 1];

    }
}
```

leetcode 63
跟前一题一样 障碍就是直接写0
如果最左最右的有石头 就不能继续往下了

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        if (obstacleGrid[m-1][n-1] == 1 || obstacleGrid[0][0] == 1) return 0; //起始和结尾有石头

        for (int i = 0; i < n; i++) {
            if (obstacleGrid[0][i] == 1) break;
            dp[0][i] = 1;
        }
        for (int i = 0; i < m; i++) {
            if (obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for (int row = 1; row < m; row++) {
            for (int column = 1; column < n; column++) {
                if (obstacleGrid[row][column] == 0) {
                    dp[row][column] = dp[row][column - 1] + dp[row - 1][column];
                } 
            }
        }

        return dp[m - 1][n - 1];
    }
}
```
