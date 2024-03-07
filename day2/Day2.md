#Day 2: 代码随想录算法训练营

## Topic:
- Array
- Sliding Window

## Summary:
- 第一第二题能够成功AC， 但是debug上面卡了一会。 第三题还是看题解慢慢体会逻辑后， 顺利解出
- 写代码时候要静下心， 不然后面debug会有很多显而易见的小错误， 反而会浪费很多时间去找那些错误。
- 双指针和滑动窗口，如果定义成一句话：指针会定义新的数组（left - right就是一个新数组） 或者 （0 - left 成为一个新数组）
- 数组中的算法： 双指针， 滑动窗口， 二分法。 其中滑动窗口还需要多加练习。
- 有时候暴力法也很考研细节和代码掌握程度。 以后可以先找到暴力法再一步一步优化
- 操控指针要多加注意
- 循环不变量原则。 如果坚持左闭右闭 就保持一贯的思想 才能解出

## Leetcode 977.有序数组的平方：
**[Problem](https://leetcode.cn/problems/squares-of-a-sorted-array/)**

**[Recourse](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html)**

Solution:
``` Java
class Solution {
    public int[] sortedSquares(int[] nums) {
        /*
        // brute force
        // 把每一个元素都平方 然后排序
        // O(n log n)
        for(int i = 0; i < nums.length; i++) {
            nums[i] *= nums[i];
        }

        Arrays.sort(nums);

        return nums;
        */

        //双指针 O(n)

        //开辟一个新数组
        int[] res = new int[nums.length];
        int index = res.length - 1;

        //一个指向头一个指向尾巴
        int left = 0;
        int right = nums.length - 1;

        while(left <= right) {
            if (nums[left] * nums[left] > nums[right] * nums[right]) {
                res[index--] = nums[left] * nums[left];
                left++;
            } else {
                res[index--] = nums[right] * nums[right];
                right--; 
            }
        }
        
        return res;
    }
}
```

## Leetcode  209.长度最小的子数组：
**[Problem](https://leetcode.cn/problems/minimum-size-subarray-sum/)**

**[Recourse](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html)**

Solution:
``` java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        /*
        //brute force O(n^2)
        int res = Integer.MAX_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int sum = 0;
            for (int j = i ; j < nums.length; j++) {
                sum += nums[j];

                if (sum >= target) {
                    res = Math.min(res, j - i + 1);
                    break;
                }
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
        */

        // sliding window O(n)

        int left = 0;
        int right = 0;
        int res = Integer.MAX_VALUE;
        int sum = 0;
        for (; right < nums.length; right++) {
            sum += nums[right];
            while (sum >= target) {
                res = Math.min(res, right - left + 1); // 当满足条件时，窗口起始位置往右滑动
                sum -= nums[left++];
            }
        }

        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```
## Leetocode  59.螺旋矩阵II
**[Problem](https://leetcode.cn/problems/spiral-matrix-ii/)**

**[Recourse](https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html)**

Solution:
``` java
// 感谢大神 Krahets 给的题解
class Solution {
    public int[][] generateMatrix(int n) {
        int l = 0, r = n - 1, t = 0, b = n -1;
        int[][] res = new int[n][n];
        int count = 1;
        int target = n * n;
        while (count <= target) {
            for (int i = l; i <= r; i++) res[t][i] = count++; // 从左往右填满
            t++;
            for (int i = t; i <= b; i++) res[i][r] = count++; // 从上往下填满
            r--;
            for (int i = r; i >= l; i--) res[b][i] = count++; // 从右往左填满
            b--;
            for (int i = b; i >= t; i--) res[i][l] = count++; // 从下往上填满
            l++;
            // 当代码运行到这里时， 已经填满一整圈。然后去填内圈
        }
        return res;
    }
}
```

















