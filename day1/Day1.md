# Day 1: 代码随想录训练营

## Tips:
- Check constraints first
- Identify keywords from the problem

## 总结：
- 当时间复杂度为 $O(n^2)$, 可以用双指针法降低时间复杂度到 $O(n)$
- 在看当问题是， 不要着急开始写代码。 最好能够在纸上写出大概流程或者伪代码。 这样可以避免很多简单的逻辑错误
- 提高语言的熟悉程度

## Topics Covered:
- Array
- Binary Search
- Two Pointer

## Resources:
- [Article Explanation](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)
- [Video Explanation](https://www.bilibili.com/video/BV1fA4y1o715)

## LeetCode Problems:
1. [704. Binary Search](https://leetcode.com/problems/binary-search/)
2. [27. Remove Element](https://leetcode.com/problems/remove-element/)

---

### Solution for Leetcode 704:

#### Idea:
- Sorted array
- Non-duplicate elements
- n in [1,10000]
- Use binary search.
Key problem: to define the range of searched range.

**左闭右闭**
```java
class Solution {
    public int search(int[] nums, int target) {
        // Time: O(log n), Space: O(1)
        if (nums[0] > target || nums[nums.length - 1] < target) return -1; // Target not in the range

        int left = 0; // Left pointer
        int right = nums.length - 1; // Right pointer

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > target) {
                right = mid - 1; // Move the right pointer when the middle value is greater than the target
            } else if (nums[mid] < target) {
                left = mid + 1; // Move the left pointer when the middle value is less than the target
            } else {
                return mid;
            }
        }

        return -1;
    }
}
```
**左闭右开**
``` Java
class Solution {
    public int search(int[] nums, int target) {
        // Time: O(log n), Space: O(1)
        if (nums[0] > target || nums[nums.length - 1] < target) return -1; // Target not in the range

        int left = 0; // Left pointer
        int right = nums.length ; // Right pointer

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > target) {
                right = mid;    // Move the right pointer when the middle value is greater than the target
            } else if (nums[mid] < target) {
                left = mid + 1;    // Move the left pointer when the middle value is less than the target
            } else {
                return mid;
            }
        }

        return -1;
    }
}
```

**Refection:**
Incorporating a check for the target's range before binary search improves efficiency

### Solution for Leetcode 27:

#### Approach: Brute Force
``` Java
class Solution {
    public int removeElement(int[] nums, int val) {
        // n < 100 可以用 暴力法 O(n^2)
        int size = nums.length;

        for (int i = 0; i < size; i++) {
            if (nums[i] == val) {
                // swap value 
                for (int j = i + 1; j < size; j++) {
                    nums[j-1] = nums[j];
                }
                i--;
                size--;
            }
        }
        return size;
    }
}
```
**Reflection**
- In the loop, I should use the `size` variable, not `nums.length`, as it caused an infinite loop.

#### Approach: Two Pointer
``` Java
class Solution {
    public int removeElement(int[] nums, int val) {
        // two pointers O(n^2) -> O(n)
        int slow = 0;
        int fast = 0;
        
        for (; fast < nums.length; fast++) {
            if (nums[fast] != val) {
                nums[slow++] = nums[fast];
            }
        }
        return slow;

    }
}
```
**Reflection**
- when a problem has a solution of time complexity O(n^2), try two pointers.
- "定义快慢指针: 快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组. 慢指针：指向更新 新数组下标的位置" (卡哥)


#### ChatGPT: 最直白的算法
``` Java
class Solution {
    public int removeElement(int[] nums, int val) {
        // O(n)
        int res = nums.length;
        int i = 0;
        while (i < res) {
            if (nums[i] == val) {
                nums[i] = nums[res - 1];
                res--;
            } else {
                i++;
            }
        }
        return res;
    }
}
```



