# Day 27: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- 当能找到局部最优的时候 一切都清晰可见
- 卡在了第三题 判别什么时候要加jump的时候
- 解题的思路不是一天两天能练出来。只能慢慢培养。 懂了就是懂了，不懂就耐心品味

## Leetcode Problem
[Recourse](https://programmercarl.com/0122.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAII.html)

Leetcode 122

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 只要今天的价格比昨天高 我就穿越回去买
        int profit = 0;
        if (prices.length < 1) return profit;

        for (int i = 1; i < prices.length; i++) {
            if (prices[i] - prices[i - 1] > 0 ) {
                profit += prices[i] - prices[i - 1];
            }
        }

        return profit;
    }
}
```

leetcode 55

借用卡哥的图
![image](https://github.com/kkkkevx/DSA/assets/108632304/20d35d8d-0849-4bd7-b53a-3c5a9c87d26f)

```java
class Solution {
    public boolean canJump(int[] nums) {
        // 问题的关键点在0
        // 思路是对的 但是细节可以在琢磨下 能AC
        // if (nums.length == 1) return true;
        // if (nums[0] == 0) return false;
        // int prev = nums[0];

        // for (int i = 1; i < nums.length; i++) {
        //     prev--;
        //     if (prev >= (nums.length - i - 1)) {
        //         return true; 
        //     }
        //     if (nums[i] == 0 && prev == 0) return false;
        //     if (nums[i] > prev) {
        //         prev = nums[i];
        //     }
        // }

        // return false;
        /**
        寻找cover 就跳最远的
         */
        if (nums.length == 1) return true;
        int cover = 0;
        for (int i = 0; i <= cover ; i++) {
            cover = Math.max(cover, nums[i] + i);
            if (cover >= nums.length - 1) return true;
        }

        return false;

    }
}
```

leetcode 45
当走出上一个覆盖最大范围的时候 才往后跳一步 因为后面的最大步数肯定cover了前面的最大步数
```java
class Solution {
    public int jump(int[] nums) {
        if (nums.length == 1) return 0;
        int curJump = 0;
        int cover = 0;
        int res = 0;
        for (int i = 0; i <= cover; i++) {
            cover = Math.max(cover, nums[i] + i);
            // 先判断能不能到最后一步 算上当先的jump 一步可以到末尾
            if (cover >= nums.length - 1) {
                res++;
                break;
            };
            // 走到当前覆盖的最大区域时，更新下一步可达的最大区域
            if (i == curJump) {
                res++;
                curJump = cover;
            }
        }
        return res;
    }
}
```
