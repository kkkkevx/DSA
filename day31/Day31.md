# Day 31: 代码随想录算法训练营

## Topic:
- Greedy Algo

## Summary
- **想清楚局部最优，想清楚全局最优，感觉局部最优是可以推出全局最优，并想不出反例，那么就试一试贪心**
- Last day for greedy algo.
- java char其实是ASCII的数值可以做加一减一的操作。

## Leetcode Problem
[Recourse](https://programmercarl.com/0738.%E5%8D%95%E8%B0%83%E9%80%92%E5%A2%9E%E7%9A%84%E6%95%B0%E5%AD%97.html)

leetcode 738
```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        String s = String.valueOf(n);
        char[] c = s.toCharArray();
        int start = s.length();

        // find out the invalid number which is larger that n[i+1]
        for (int i = s.length() - 2; i >= 0; i--) {
            if (c[i] > c[i + 1]) {
                c[i]--;
                start = i + 1;
            }
        }

        // change number to 9
        for (int i = start; i < s.length(); i++) {
            c[i] = '9';
        }

        return Integer.parseInt(String.valueOf(c));
    }
}
```
