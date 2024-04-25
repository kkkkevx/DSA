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
- 计算机的真谛就是穷举
- 算法的真谛就是进行聪明的穷举
 
## Leetcode Problem

leetcode 139
```
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        /*
            dp[i] 代表前i个字符可以被dict组合
            状态转移方程： dp[j]是否为true和剩下的 j--i的字符能否被dict组成
        */
        Set<String> dict = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }
}
```
