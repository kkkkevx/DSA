# Day 28: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- 思路有但还是有反面例子， 但是在思考的过程还是很有帮助
- Understand the Problem Deeply
- try brutal force and be better step by step
- after finish coding, write some comment to have better understanding. it also a good habit when i work within a team.

## Leetcode Problem
[Recourse](https://programmercarl.com/1005.K%E6%AC%A1%E5%8F%96%E5%8F%8D%E5%90%8E%E6%9C%80%E5%A4%A7%E5%8C%96%E7%9A%84%E6%95%B0%E7%BB%84%E5%92%8C.html#%E6%80%9D%E8%B7%AF)

Leetcode 100
```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        /**
        第一次排序把负数都转成正数
        第二次排序基数k值 双数不管 单数 sum-2倍的最小值
        优化可以只调用一次排序， 在第一遍的时候就记录最小绝对值
         */
        Arrays.sort(nums);
        int sum = 0;
        int minIndex = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] < 0 && k > 0) {
                nums[i] = -nums[i];
                k--;
            }
            sum += nums[i];
            minIndex = nums[i] < nums[minIndex] ? i : minIndex; // 优化
        }
        // Arrays.sort(nums);
        if (k % 2 == 0) {
            return sum;
        } else{
            return sum - 2 * nums[minIndex];
        }
             
    }
}
```

Leetcode 134
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        // 初始化总油量和总耗油量，以判断全程是否有可能完成
        int totalGas = 0;
        int totalCost = 0;
        // tank用于追踪从当前起点出发的油量差额
        int tank = 0;
        // res记录可能的起点
        int res = 0;
        for (int i = 0; i < gas.length; i++) {
            totalGas += gas[i];
            totalCost += cost[i];
            tank += gas[i] - cost[i];
            // 如果tank变为负数，意味着无法从当前起点到达下一个加油站
            // 因此，需要更换起点为i+1，并重置tank
            if (tank < 0) {
                tank = 0;
                res = i + 1;
            }
        }
        // 如果总油量大于等于总耗油量，返回起点索引，否则返回-1
        return totalGas >= totalCost ? res : -1;
    }
}
```

Leetcode 135
```java
class Solution {
    public int candy(int[] ratings) {
        // record candy for each child
        int[] candies = new int[ratings.length];
        // every one get at least one
        candies[0] = 1;
        for (int i = 1; i < ratings.length; i++) {
            candies[i] = 1;

            // if right child better than left, give right child one more
            if (ratings[i] > ratings[i - 1]) {
                candies[i] = candies[i - 1] + 1;
            }
        }

        for (int i = ratings.length - 2; i >= 0; i--) {
            // if left child better than right, give left child max number compare to right child + 1 or original he got.
            if (ratings[i] > ratings[i + 1]) {
                candies[i] = Math.max(candies[i], candies[i + 1] + 1);
            }
        }

        int sum = 0;
        for (int candy : candies) {
            sum += candy;
        }
        return sum;

    }
}
```
