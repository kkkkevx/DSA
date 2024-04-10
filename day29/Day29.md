# Day 29: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- 贪心真的没法说 只能多练多锻炼思路
- 今天有多用到lambda 表示法去写排序
  - (a,b) -> return a - b 升序 b和a换位置就是降序

## Leetcode Problem
[Recourse](https://programmercarl.com/0860.%E6%9F%A0%E6%AA%AC%E6%B0%B4%E6%89%BE%E9%9B%B6.html)

Leetcode 860
这道题比较考验写代码的思路清晰程度
```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int[] cash = new int[3];

        for (int i = 0; i < bills.length; i++) {
            if (bills[i] == 5) {
                cash[0] += 1;
            } else if (bills[i] == 10) {
                cash[1] += 1;
                if (cash[0] > 0) {
                    cash[0] -= 1;
                } else {
                    return false;
                }
            } else {
                cash[2] += 1;
                if (cash[1] > 0 && cash[0] > 0) {
                    cash[0] -= 1;
                    cash[1] -= 1;
                } else if (cash[0] > 2) {
                    cash[0] -= 3;
                } else {
                    return false;
                }
            }
        }

        return true;
    }
}
```

Leetcode 406
先确定一个系数在确定另一个 需要排序
```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        // 先排身高 如果身高一样 k小在前
        Arrays.sort(people, (a ,b) -> {
            if (a[0] == b[0]) return a[1] - b[1]; // 如果身高相同用 k排序 升序
            return b[0] - a[0]; // 降序
        });

        List<int[]> que = new LinkedList<>();

        // 按照k值插入
        for (int[] p : people) {
            que.add(p[1], p);
        }

        return que.toArray(new int[people.length][]);
    }
}
```

Leetcode 452

重叠问题可以考虑先排序 然后在把图画出来 会很清晰
```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        Arrays.sort(points, (a, b) -> 
            Integer.compare(a[0], b[0]) // 升序按照气球的气球的起始点
        );
        int res = 1;
        for (int i = 1; i < points.length; i++) {
            if (points[i][0] > points[i-1][1]) { //气球不重叠 可以射前面那个了
                res++;
            } else {
                points[i][1] = Math.min(points[i - 1][1], points[i][1]); //气球重叠 先不射看看后面那个会不会也重叠
            }
        }

        return res;
    }
}
```
