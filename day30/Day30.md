# Day 30: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- 今天都是重叠区间问题，在写代码之前理清思路把图画出来会很好理解。

## Leetcode Problem
[https://leetcode.cn/problems/non-overlapping-intervals/](https://programmercarl.com/0435.%E6%97%A0%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4.html)


leetcode 435
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        // 局部最优 选第一个然后开始找不重叠的
        // 排序之后找右边界
        int res = 1;
        Arrays.sort(intervals, (a, b) -> {
            return a[1] - b[1];
        });
        int end = intervals[0][1];


        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] >= end) { //找到不重叠部分
                end = intervals[i][1];
                res++;
            } 
        }

        return intervals.length - res;
    }
}
```

leetcode 763
第一遍遍历找到每个字母最后一次出现的位置
第二遍遍历找到第一个字母的最远边界 如果在边界内有更远的就更新最远边界， 当到最远边界就说明 可以分割了
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> res = new ArrayList<>();

        int[] dict =new int[26]; // record last occurrence
        int left = 0;
        int right = 0;
        for (int i = 0; i < s.length(); i++) {
            dict[s.charAt(i) - 'a'] = i;
        }

        for (int i = 0; i < s.length(); i++) {
            right = Math.max(right, dict[s.charAt(i) - 'a']); // find the max right bound
            if (i == right) {
                res.add(right - left + 1);
                left = i + 1;
            }
        }

        return res;
    }
}
```

Leetcode 56
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        // sort by left number
        Arrays.sort(intervals, (a, b) -> {
            return a[0] - b[0];
        });

        List<int[]> res = new ArrayList<>();
        // first interval
        int left = intervals[0][0];
        int right = intervals[0][1];

        for (int i = 1; i < intervals.length; i++) {
            // overlap, move the right bound
            if (intervals[i][0] <= right) {
                right = Math.max(right, intervals[i][1]);
            } else { // not overlap, add to res and start new interval
                res.add(new int[]{left, right});
                left = intervals[i][0];
                right = intervals[i][1];
            }
        }
        // add the last interval
        res.add(new int[]{left, right});
        return res.toArray(new int[res.size()][]);
    }
}
```
