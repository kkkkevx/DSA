# Day 26: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- 不要脑洞模拟 千万别相信自己的脑子  还是写下或者run一run
- 保持写代码前把思路计划好。  计划虽然不一定能成功但是一定要有。

## Leetcode Problem
[Recourse](https://programmercarl.com/0455.%E5%88%86%E5%8F%91%E9%A5%BC%E5%B9%B2.html#%E6%80%9D%E8%B7%AF)

Leetcode 455
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        int res = 0;
        Arrays.sort(g);
        Arrays.sort(s);
        int index = 0;
        for (int cookie : s) {
            if (index < g.length && cookie >= g[index]) {
                index++;
                res++;
            }
        }
        return res;
    }
}
```

Leetccode 376
```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if (nums.length < 2) return 1;
        int res = 0;
        int prev = -1;
        for (int i = 1; i< nums.length; i++) {
            int diff = nums[i-1] - nums[i];
            if (diff > 0 && prev != 1) {
                res++;
                prev = 1;
            } else if (diff < 0 && prev != 0) {
                res++;
                prev = 0;
            }
        }

        return res + 1;
    }
}
```

Leetcode 53
if sum below than 0, restart. only looking for positive sum
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = Integer.MIN_VALUE;
        int sum = 0;
        for (int num : nums) {
            sum += num;
            if (sum > res) {
                res = sum;
            }
            if (sum < 0) {
                sum = 0;
            }
        }

        return res;
    }
}
```
